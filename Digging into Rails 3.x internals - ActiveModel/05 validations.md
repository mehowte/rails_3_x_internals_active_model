!SLIDE code small
# Don't store invalid data
    
    @@@ ruby
      class User
        (...)
        validates :name, :age, :presence => true
        validates :age, :numericality => true
      end
      #also we need id presence validation by default 
      
      # user is an instance of User
      user.valid?
      user.save # should be false when invalid
      user.update_attributes # same here
      user.create # and here
      user.errors # should not be empty when invalid

!SLIDE code small
# Validations

    @@@ ruby
    module FileRecord
      class Base

        include AttributeManagement
        include Persistence
        ...




        attributes :id


        def initialize(attributes = {})
          self.attributes = attributes 
        end
      end
    end

!SLIDE code small
# Validations

    @@@ ruby
    module FileRecord
      class Base

        include AttributeManagement
        include Persistence
        include Validations




        attributes :id


        def initialize(attributes = {})
          self.attributes = attributes 
        end
      end
    end

!SLIDE code smaller
# Validations

    @@@ ruby
    module FileRecord::Validations
        extend ActiveSupport::Concern
        
        ...










    end

!SLIDE code smaller
# Validations

    @@@ ruby
    module FileRecord::Validations
        extend ActiveSupport::Concern
        
        include ActiveModel::Validations

        ...








    end

!SLIDE code smaller
# Validations

    @@@ ruby
    module FileRecord::Validations
        extend ActiveSupport::Concern
        
        include ActiveModel::Validations

        def save
          if valid?
            super
            true
          else
            false
          end
        end

    end

!SLIDE code small
# Validations

    @@@ ruby
    module FileRecord
      class Base

        include AttributeManagement
        include Persistence
        include Validations




        attributes :id
        ...

        def initialize(attributes = {})
          self.attributes = attributes 
        end
      end
    end

!SLIDE code small
# Validations

    @@@ ruby
    module FileRecord
      class Base

        include AttributeManagement
        include Persistence
        include Validations




        attributes :id
        validates :id, :presence => true

        def initialize(attributes = {})
          self.attributes = attributes 
        end
      end
    end
