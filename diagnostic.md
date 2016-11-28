# Rails API Relationships Diagnostic

Place your responses inside the fenced code-blocks where indivated by comments.

1.  Describe a reason why a join tables may be valuable.

```md
They allow for easy access to relational data and also help seperate data which then allows for better management and organization.
```

1.  Provide a database table structure and explain the Entity Relationship that
describes a many-to-many relationship for `Profiles`, `Movies` and `Favorites`
(Think of Netflix). A `Profile` has a `given_name`, `surname` and `email` and a
`Movies` have `title`, `release_date`, and `length` and `Favorites` would be the
join table with references to `Movies` and `Profiles`.

```sh
Profiles have many Movies through Favorites and Movies have many Profiles through Favorites
```

1.  For the above example, what needs to be added to the Model files?

```rb
class Profile < ActiveRecord::Base
has_many Movies, through: :favorites
has_many Movies
end
```

```rb
class Movie < ActiveRecord::Base
has_many Profiles, through: :favorites
has_many Favorites
end
```

```rb
class Favorite < ActiveRecord::Base
belongs_to :movie, inverse_of :profile
belongs_to :profile, inverse_of :movie
end
```

1.  What is the purpose of a serializer? What would our `Profile` serializer look
like to show all movies favorited by a profile on
`http://localhost:3000/profiles/1`

```sh
it acts as a data filter
```

```rb
class ProfileSerializer < ActiveModel::Serializer
  attributes :given_name, :surname, :email
end
```

1.  What would the command be to _scaffold_ out a **join table** for Favorites from
the above `Movies` and `Profiles`.

```sh
rails g scaffold Favorites references:movie references:profile
```

1.  What is `Dependent: Destroy` and where/why would we use it?

```sh
It created conditionals so as not to allow orphaned table values. It
```

1.  Think of **ANY** example where you would have a one-to-many relationship as well
as a many-to-many relationship in an application. You only need to list the
description about the resources and how they relate to one another.

```sh

```
