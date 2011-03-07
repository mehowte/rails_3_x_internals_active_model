!SLIDE code small
# even more attribute magic

    @@@ ruby
    user.changed?
    user.changes 
    user.name_changed?
    user.age_was
    (...)


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
          ...
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

!SLIDE code smaller
# Changes...

    @@@ ruby
    module FileRecord
      module AttributeMethods
        module Dirty
          extend ActiveSupport::Concern

          ...













        end
      end
    end

!SLIDE code smaller
# Changes...

    @@@ ruby
    module FileRecord
      module AttributeMethods
        module Dirty
          extend ActiveSupport::Concern

          include ActiveModel::Dirty

          ...











        end
      end
    end

!SLIDE code smaller
# Changes...

    @@@ ruby
    module FileRecord
      module AttributeMethods
        module Dirty
          extend ActiveSupport::Concern

          include ActiveModel::Dirty

          def save
            if status = super
              @previously_changed = changes
              @changed_attributes.clear
            end
            status
          end

          ...



        end
      end
    end

!SLIDE code smaller
# Changes...

    @@@ ruby
    module FileRecord
      module AttributeMethods
        module Dirty
          extend ActiveSupport::Concern

          include ActiveModel::Dirty

          def save
            if status = super
              @previously_changed = changes
              @changed_attributes.clear
            end
            status
          end

          def attribute=(name, value)
            attribute_will_change!(name) if attributes[name] != value
            super(name, value)
          end
        end
      end
    end
