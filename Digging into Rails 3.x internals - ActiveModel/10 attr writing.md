!SLIDE code smaller
# Attribute writing methods

    @@@ ruby
    module FileRecord
      module AttributeMethods
        module Write
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
# Attribute writing methods

    @@@ ruby
    module FileRecord
      module AttributeMethods
        module Write
          extend ActiveSupport::Concern
          include ActiveModel::AttributeMethods

          included do
            attribute_method_suffix "="

          end

          protected
          ...






        end
      end
    end

!SLIDE code smaller
# Attribute writing methods

    @@@ ruby
    module FileRecord
      module AttributeMethods
        module Write
          extend ActiveSupport::Concern
          include ActiveModel::AttributeMethods

          included do
            attribute_method_suffix "="
            ...
          end

          protected
          def attribute=(name, value)
            @attributes[name] = value
          end




        end
      end
    end

!SLIDE code smaller
# Attribute writing methods

    @@@ ruby
    module FileRecord
      module AttributeMethods
        module Write
          extend ActiveSupport::Concern
          include ActiveModel::AttributeMethods

          included do
            attribute_method_suffix "="
            attribute_method_prefix "clear_"
          end

          protected
          def attribute=(name, value)
            @attributes[name] = value
          end

          ...


        end
      end
    end

!SLIDE code smaller
# Attribute writing methods

    @@@ ruby
    module FileRecord
      module AttributeMethods
        module Write
          extend ActiveSupport::Concern
          include ActiveModel::AttributeMethods

          included do
            attribute_method_suffix "="
            attribute_method_prefix "clear_"
          end

          protected
          def attribute=(name, value)
            @attributes[name] = value
          end

          def clear_attribute(attribute)
            send(:"#{attribute}=", nil)
          end
        end
      end
    end
