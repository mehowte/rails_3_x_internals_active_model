!SLIDE code smaller
# Concern - a useful pattern

    @@@ ruby
    module X
      extend ActiveSupport::Concern
      ...









    end
    class Y
      include X
    end




!SLIDE code smaller
# Concern - a useful pattern

    @@@ ruby
    module X
      extend ActiveSupport::Concern
      included do
        puts self.to_s # will print "X" later on
      end
      ...






    end
    class Y
      include X
    end
    ...



!SLIDE code smaller
# Concern - a useful pattern

    @@@ ruby
    module X
      extend ActiveSupport::Concern
      included do
        puts self.to_s # will print "X" later on
      end
      module ClassMethods
        def a; end
      end
      ...



    end
    class Y
      include X
    end
    Y.respond_to? :a #=> true
    ...


!SLIDE code smaller
# Concern - a useful pattern

    @@@ ruby
    module X
      extend ActiveSupport::Concern
      included do
        puts self.to_s # will print "X" later on
      end
      module ClassMethods
        def a; end
      end
      module InstanceMethods
        def b; end
      end
      ...
    end
    class Y
      include X
    end
    Y.respond_to? :a #=> true
    Y.new.respond_to? :b #=> true
    ...


!SLIDE code smaller
# Concern - a useful pattern

    @@@ ruby
    module X
      extend ActiveSupport::Concern
      included do
        puts self.to_s # will print "X" later on
      end
      module ClassMethods
        def a; end
      end
      module InstanceMethods
        def b; end
      end
      def c; end
    end
    class Y
      include X
    end
    Y.respond_to? :a #=> true
    Y.new.respond_to? :b #=> true
    Y.new.respond_to? :c #=> true
