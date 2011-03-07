Digging into Rails 3.x internals - ActiveModel
==========
Presentation describing step by step implementation of [FileRecord][1] library.
It illustrates usage of ActiveModel library as well as good practices of extracting functionalities into separate modules. 

FileRecord is a simplistic clone of ActiveRecord, fully compatible with ActiveModel.

You can see presentation on [heroku][0] or install and run locally.

Installation
------------

    git clone git://github.com/mehowte/rails_3_x_internals_active_model.git
    cd rails_3_x_internals_active_model
    bundle install

Running presentation
-------

    showoff serve

Implementation and Demo app
--------

You can find FileRecord library along with tests and demo app [here on github][1].

License
-------
Copyright 2011 Michal Taszycki

This presentations is released under an [attribution and non-commercial Creative Commons License](http://creativecommons.org/licenses/by-nc/3.0/pl/deed.en).

History
-------
Presented at KRUG (Kraków Ruby User Group) meeting, Poland 2011-03-01

[0]: http://rails-3-internals-active-model.heroku.com/
[1]: https://github.com/mehowte/rails_3_x_internals_active_model

