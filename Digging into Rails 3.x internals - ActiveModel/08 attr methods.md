!SLIDE code small
# attribute magic

    @@@ ruby
    user.name = "Joe"
    user.is_age_valid? 
    user.clear_name
    user.age

!SLIDE code small
# We need...

    @@@ ruby
    module FileRecord
      class Base

        include AttributeManagement
        include Persistence
        include Validations
        include Callbacks
        ...


        attributes :id
        validates :id, :presence => true

        def initialize(attributes = {})
          self.attributes = attributes 
        end
      end
    end

!SLIDE code small
# ... lot's of attribute methods
    
    @@@ ruby
    module FileRecord
      class Base

        include AttributeManagement
        include Persistence
        include Validations
        include Callbacks
        include AttributeMethods:All


        attributes :id
        validates :id, :presence => true

        def initialize(attributes = {})
          self.attributes = attributes 
        end
      end
    end


!SLIDE code smaller
# Attribute methods

## Can't stop extracting modules...

    @@@ ruby
    module FileRecord
      module AttributeMethods

        module All
          extend ActiveSupport::Concern
  
          include Read
          include Write
          include Validation
          include Dirty
        end
      end
    end
