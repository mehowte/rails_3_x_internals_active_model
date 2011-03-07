!SLIDE code small
# Could we get a CRUD with that

    @@@ ruby
      User.find(id)
      User.all
      User.create
      
      # user is an instance of User
      user.save
      user.destroy
      user.update_attributes
      # also user should have an id attribute by default
        


!SLIDE code small
# Persistence

    @@@ ruby
    module FileRecord
      class Base

        include AttributeManagement
        ...





        ...


        def initialize(attributes = {})
          self.attributes = attributes 
        end
      end
    end

!SLIDE code small
# Persistence

    @@@ ruby
    module FileRecord
      class Base

        include AttributeManagement
        ...





        attributes :id


        def initialize(attributes = {})
          self.attributes = attributes 
        end
      end
    end

!SLIDE code small
# Persistence

    @@@ ruby
    module FileRecord
      class Base

        include AttributeManagement
        include Persistence





        attributes :id


        def initialize(attributes = {})
          self.attributes = attributes 
        end
      end
    end

!SLIDE code smaller
# Persistence class methods

    @@@ ruby
    module FileRecord::Persistence
      extend ActiveSupport::Concern
      ...

      module ClassMethods



















      end
    end

!SLIDE code smaller
# Persistence class methods

    @@@ ruby
    module FileRecord::Persistence
      extend ActiveSupport::Concern
      include ActiveModel::Serializers::JSON

      module ClassMethods
















        ...


      end
    end

!SLIDE code smaller
# Persistence class methods

    @@@ ruby
    module FileRecord::Persistence
      extend ActiveSupport::Concern
      include ActiveModel::Serializers::JSON

      module ClassMethods
        ...















        def filename(name)
          "tmp/file_records/" + name
        end
      end
    end

!SLIDE code smaller
# Persistence class methods

    @@@ ruby
    module FileRecord::Persistence
      extend ActiveSupport::Concern
      include ActiveModel::Serializers::JSON

      module ClassMethods
        def find(name)
          return nil unless File.exists? filename(name)
          self.new.from_json(File.read(filename(name)))
        end

        ...










        def filename(name)
          "tmp/file_records/" + name
        end
      end
    end

!SLIDE code smaller
# Persistence class methods

    @@@ ruby
    module FileRecord::Persistence
      extend ActiveSupport::Concern
      include ActiveModel::Serializers::JSON

      module ClassMethods
        def find(name)
          return nil unless File.exists? filename(name)
          self.new.from_json(File.read(filename(name)))
        end

        def all
          Dir.new("tmp/file_records").entries.reject do |name|
            File.directory?(name)  
          end.map { |name| find(name) }
        end
          
        ...




        def filename(name)
          "tmp/file_records/" + name
        end
      end
    end

!SLIDE code smaller
# Persistence class methods

    @@@ ruby
    module FileRecord::Persistence
      extend ActiveSupport::Concern
      include ActiveModel::Serializers::JSON

      module ClassMethods
        def find(name)
          return nil unless File.exists? filename(name)
          self.new.from_json(File.read(filename(name)))
        end

        def all
          Dir.new("tmp/file_records").entries.reject do |name|
            File.directory?(name)  
          end.map { |name| find(name) }
        end
          
        def create(attributes = {})
          obj = self.new(attributes)
          obj.save ? obj : nil
        end

        def filename(name)
          "tmp/file_records/" + name
        end
      end
    end


!SLIDE code smaller
# Persistence instance methods

    @@@ ruby
    module FileRecord::Persistence

      (...)

      ...


















    end

!SLIDE code smaller
# Persistence instance methods

    @@@ ruby
    module FileRecord::Persistence

      (...)

      def persisted?
        id && File.exists?(self.class.filename(id))
      end

      ...














    end

!SLIDE code smaller
# Persistence instance methods

    @@@ ruby
    module FileRecord::Persistence

      (...)

      def persisted?
        id && File.exists?(self.class.filename(id))
      end

      def save
        File.open(self.class.filename(id), 'w') do |f| 
          f.write(to_json) 
        end 
      end

      ...








    end

!SLIDE code smaller
# Persistence instance methods

    @@@ ruby
    module FileRecord::Persistence

      (...)

      def persisted?
        id && File.exists?(self.class.filename(id))
      end

      def save
        File.open(self.class.filename(id), 'w') do |f| 
          f.write(to_json) 
        end 
      end

      def destroy
        File.delete(self.class.filename(id)) if persisted?
      end

      ...




    end

!SLIDE code smaller
# Persistence instance methods

    @@@ ruby
    module FileRecord::Persistence

      (...)

      def persisted?
        id && File.exists?(self.class.filename(id))
      end

      def save
        File.open(self.class.filename(id), 'w') do |f| 
          f.write(to_json) 
        end 
      end

      def destroy
        File.delete(self.class.filename(id)) if persisted?
      end

      def update_attributes(attributes)
        @attributes.merge!(attributes)
        sanitize_attributes
        save
      end
    end

