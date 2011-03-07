!SLIDE code small
# Let's start from basics
    @@@ ruby
    class User < FileRecord::Base
      attributes :name, :age

      def initialize(attrs = {})
        super(attrs)
      end
    end
    
    u = User.new(:name => "John", 
                 :age => 12, 
                 :question => "What is this?")
    u.attributes #=> {:name => "John", :age => 12}
    u.attributes = {:name => "Jane", 
                    :age => 22, 
                    :loves => "Tarzan"}
    u.attributes #=> {:name => "Jane", :age => 22}


!SLIDE code small
# We need some...

    @@@ ruby
    module FileRecord
      class Base

        ...












      end
    end

!SLIDE code small
# AttributeManagement

    @@@ ruby
    module FileRecord
      class Base

        include AttributeManagement












      end
    end

!SLIDE code smaller
# AttributeManagement class methods

    @@@ ruby
    module FileRecord
      module AttributeManagement
        extend ActiveSupport::Concern

        included do
          ...



        end

        module ClassMethods
          ...



        end

        (...)

      end
    end

!SLIDE code smaller
# AttributeManagement class methods

    @@@ ruby
    module FileRecord
      module AttributeManagement
        extend ActiveSupport::Concern

        included do
          class_attribute :_attribute_names 
          self._attribute_names = []

          attr_reader :attributes
        end

        module ClassMethods
          ...



        end

        (...)

      end

!SLIDE code smaller
# AttributeManagement class methods

    @@@ ruby
    module FileRecord
      module AttributeManagement
        extend ActiveSupport::Concern

        included do
          class_attribute :_attribute_names 
          self._attribute_names = []

          attr_reader :attributes
        end

        module ClassMethods
          def attributes(*attribute_names)
            self._attribute_names += attribute_names
            self._attribute_names.uniq!
          end
        end

        (...)

      end
    end

!SLIDE code smaller
# AttributeManagement instance methods

    @@@ ruby
    module FileRecord
      module AttributeManagement
        
        (...)

        ...




        ...




      end
    end

!SLIDE code smaller
# AttributeManagement instance methods

    @@@ ruby
    module FileRecord
      module AttributeManagement
        
        (...)

        def attributes=(attributes)
          @attributes = attributes
          sanitize_attributes
        end


        ...




      end
    end

!SLIDE code smaller
# AttributeManagement instance methods

    @@@ ruby
    module FileRecord
      module AttributeManagement
        
        (...)

        def attributes=(attributes)
          @attributes = attributes
          sanitize_attributes
        end

        def sanitize_attributes
          @attributes.keep_if do |name, value| 
            self.class._attribute_names.include? name.to_sym
          end
        end

      end
    end

!SLIDE code small
# AttributeManagement

    @@@ ruby
    module FileRecord
      class Base

        include AttributeManagement






        


        ...


      end
    end


!SLIDE code small
# AttributeManagement

    @@@ ruby
    module FileRecord
      class Base

        include AttributeManagement









        def initialize(attributes = {})
          self.attributes = attributes 
        end
      end
    end
