!SLIDE code small
# before, after and around

    @@@ ruby
    class User
      (...)
      before_save :do_something
      after_destroy :do_something_else
      before_validation :do_really_crazy_stuff

      protected

      def do_something
        (...)
      end

      def do_something_else
        (...)
      end

      def do_really_crazy_stuff
        (...)
      end
    end 

!SLIDE code small
# Callbacks

    @@@ ruby
    module FileRecord
      class Base

        include AttributeManagement
        include Persistence
        include Validations
        ...



        attributes :id
        validates :id, :presence => true

        def initialize(attributes = {})
          self.attributes = attributes 
        end
      end
    end


!SLIDE code small
# Callbacks

    @@@ ruby
    module FileRecord
      class Base

        include AttributeManagement
        include Persistence
        include Validations
        include Callbacks



        attributes :id
        validates :id, :presence => true

        def initialize(attributes = {})
          self.attributes = attributes 
        end
      end
    end


!SLIDE code smaller
# Callbacks

    @@@ ruby
    module FileRecord
      module Callbacks
        extend ActiveSupport::Concern
        
        included do
          ...



        end 








      end
    end

!SLIDE code smaller
# Callbacks

    @@@ ruby
    module FileRecord
      module Callbacks
        extend ActiveSupport::Concern
        
        included do
          extend ActiveModel::Callbacks
          include ActiveModel::Validations::Callbacks

          define_model_callbacks :save, :destroy
        end 

        ...






      end
    end

!SLIDE code smaller
# Callbacks

    @@@ ruby
    module FileRecord
      module Callbacks
        extend ActiveSupport::Concern
        
        included do
          extend ActiveModel::Callbacks
          include ActiveModel::Validations::Callbacks

          define_model_callbacks :save, :destroy
        end 

        def save
          run_callbacks(:save) { super }
        end

        ...


      end
    end

!SLIDE code smaller
# Callbacks

    @@@ ruby
    module FileRecord
      module Callbacks
        extend ActiveSupport::Concern
        
        included do
          extend ActiveModel::Callbacks
          include ActiveModel::Validations::Callbacks

          define_model_callbacks :save, :destroy
        end 

        def save
          run_callbacks(:save) { super }
        end

        def destroy
          run_callbacks(:destroy) { super }
        end
      end
    end

