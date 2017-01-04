# searchable
a simple php trait for laravel >= 5.0 to search in models and related models
# Installation

Simply Run the Composer require comand.

```
composer require beaumind/searchable
```

# Usage

Add the trait to your model and your search rules.

```php
use Beaumind\Searchable\Searchable;

class Post extends \Eloquent
{
    use Searchable;

    /**
     * Searchable columns.
     *
     * @var array
     */
    public $searchable_fields = [
      title,
      body,
      user.name,
      uesr.email
    ];


    public function user()
    {
        return $this->belongsTo('User');
    }

}
```
Now you can search your model.

```php
// Simple search
$posts = Post::search($query)->get();

// Search and get relations
// It will not get the relations if you don't do this
$posts = Post::search($query)
            ->with('user')
            ->get();
```
## Search Paginated

As easy as laravel default queries

```php
// Search with relations and paginate
$posts = Post::search($query)
            ->with('user')
            ->paginate(20);
```
## Mix queries

Search method is compatible with any eloquent method. You can do things like this:

```php
// Search only active posts
$posts = Post::where('status', 'active')
            ->search($query)
            ->paginate(20);
```
