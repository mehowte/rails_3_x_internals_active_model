!SLIDE code small
# Last but not least

    @@@ ruby
    module FileRecord
      class Base

        include AttributeManagement
        include Persistence
        include Validations
        include Callbacks
        include AttributeMethods:All
        ... 

        attributes :id
        validates :id, :presence => true

        def initialize(attributes = {})
          self.attributes = attributes 
        end
      end
    end

!SLIDE code small
# Wait for it...

    @@@ ruby
    module FileRecord
      class Base

        include AttributeManagement
        include Persistence
        include Validations
        include Callbacks
        include AttributeMethods:All
        ... 

        attributes :id
        validates :id, :presence => true

        def initialize(attributes = {})
          self.attributes = attributes 
        end
      end
    end

!SLIDE code small
# Yay! Compatibility

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

!SLIDE code smaller
# Compatibility

    @@@ ruby
    module FileRecord
      module Compatibility
        extend ActiveSupport::Concern

        included do    
          extend ActiveModel::Naming
          extend ActiveModel::Translation
          include ActiveModel::Conversion
        end
      end
    end
