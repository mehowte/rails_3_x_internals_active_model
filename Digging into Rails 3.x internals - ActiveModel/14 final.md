!SLIDE code small
# FileRecord::Base Final

    @@@ ruby
    module FileRecord
      class Base

        include AttributeManagement
        include Persistence
        include Validations
        include Callbacks
        include AttributeMethods:All
        include Compatibility

        attributes :id
        validates :id, :presence => true

        def initialize(attributes = {})
          self.attributes = attributes 
        end
      end
    end

!SLIDE code small
# FileRecord autoloading

    @@@ ruby
    module FileRecord
      autoload :Base, 'file_record/base'
      autoload :AttributeMethods, 'file_record/attribute_methods'
      autoload :AttributeManagement, 'file_record/attribute_management'
      autoload :Persistence, 'file_record/persistence'
      autoload :Validations, 'file_record/validations'
      autoload :Callbacks, 'file_record/callbacks'
      autoload :Compatibility, 'file_record/compatibility'
    end
