!SLIDE code smaller
# Attribute reading methods

    @@@ ruby
    module FileRecord::AttributeMethods
      module Read
        extend ActiveSupport::Concern
        ...

        included do

        end

        module ClassMethods




        end

      protected




      end
    end

!SLIDE code smaller
# Attribute reading methods

    @@@ ruby
    module FileRecord::AttributeMethods
      module Read
        extend ActiveSupport::Concern
        include ActiveModel::AttributeMethods

        included do
          
        end

        module ClassMethods
          ...



        end

      protected




      end
    end

!SLIDE code smaller
# Attribute reading methods

    @@@ ruby
    module FileRecord::AttributeMethods
      module Read
        extend ActiveSupport::Concern
        include ActiveModel::AttributeMethods

        included do
          ...
        end

        module ClassMethods
          def attributes(*args)
            super(*args)
            define_attribute_methods args
          end
        end

      protected




      end
    end

!SLIDE code smaller
# Attribute reading methods

    @@@ ruby
    module FileRecord::AttributeMethods
      module Read
        extend ActiveSupport::Concern
        include ActiveModel::AttributeMethods

        included do
          attribute_method_prefix ""
        end

        module ClassMethods
          def attributes(*args)
            super(*args)
            define_attribute_methods args
          end
        end

      protected
        ...



      end
    end

!SLIDE code smaller
# Attribute reading methods

    @@@ ruby
    module FileRecord::AttributeMethods
      module Read
        extend ActiveSupport::Concern
        include ActiveModel::AttributeMethods

        included do
          attribute_method_prefix ""
        end

        module ClassMethods
          def attributes(*args)
            super(*args)
            define_attribute_methods args
          end
        end

      protected
        def attribute(name)
          @attributes[name]
        end

      end
    end
