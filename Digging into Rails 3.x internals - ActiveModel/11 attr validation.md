!SLIDE code smaller
# Single attribute validation

    @@@ ruby
    module FileRecord
      module AttributeMethods

        module Validation
          extend ActiveSupport::Concern

          include ActiveModel::AttributeMethods

          included do
            ...

          end

          protected



        end
      end
    end

!SLIDE code smaller
# Single attribute validation

    @@@ ruby
    module FileRecord
      module AttributeMethods

        module Validation
          extend ActiveSupport::Concern

          include ActiveModel::AttributeMethods

          included do
            attribute_method_affix :prefix => 'is_', 
                                   :suffix => "_valid?"
          end

          protected
          ...


        end
      end
    end

!SLIDE code smaller
# Single attribute validation

    @@@ ruby
    module FileRecord
      module AttributeMethods

        module Validation
          extend ActiveSupport::Concern

          include ActiveModel::AttributeMethods

          included do
            attribute_method_affix :prefix => 'is_', 
                                   :suffix => "_valid?"
          end

          protected
          def is_attribute_valid?(attribute)
            valid? || errors[attribute].empty?
          end
        end
      end
    end
