activerecord-diff
=================


Simple ActiveRecord diff functionality.


Installation
------------

```
$ gem install activerecord-diff
```


Example usage
-------------

```ruby
require 'active_record/diff'

class User < ActiveRecord::Base
  include ActiveRecord::Diff
end

alice = User.create(:name => 'alice', :email_address => 'alice@example.org')

bob = User.create(:name => 'bob', :email_address => 'bob@example.org')

alice.diff?(bob)  # => true

alice.diff(bob)  # => {:name => ['alice', 'bob'], :email_address => ['alice@example.org', 'bob@example.org']}

alice.diff({:name => 'eve'})  # => {:name => ['alice', 'eve']}
```


Configuration
-------------

By default, ActiveRecord::Base.content_columns is used to decide which attributes
to compare. You can include or exclude attributes from this as follows:

```ruby
class User < ActiveRecord::Base
  diff :include => [:id], :exclude => [:password_hash]
end
```

Alternatively, you can specify exactly which columns to compare:

```ruby
class User < ActiveRecord::Base
  diff :id, :name, :email_address
end
```

Copyright
---------

To the extent possible under law, Tim Fletcher has waived all copyright and
related or neighboring rights to activerecord-diff. This work is published
from the United Kingdom. http://creativecommons.org/publicdomain/zero/1.0/
