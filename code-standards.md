# php-code-stranded

#### This is a set of programming exercises aimed at improving object-oriented design skills. These exercises provide constraints and rules to encourage developers to write more maintainable and understandable code. While not a set of strict rules, they promote principles and practices that align with good object-oriented design.

## A. Simple Rules for Simpler Code:

### 1. Only One Level of Indentation per Method
The main idea is that each method only performs one action. This way, we are making the code easier to read and maintain. In addition to promoting the Single Responsibility Principle and avoiding the Hadouken effect. You can extract behaviours for other methods by ensuring a single indentation level. By doing this, you are also applying the Extract Method Pattern.

:x:

```php
foreach ($sniffGroups as $sniffGroup) {
    foreach ($sniffGroup as $sniffKey => $sniffClass) {
        if (! $sniffClass instanceof Sniff) {
            throw new InvalidClassTypeException;
        }
    }
}
```

:+1:

```php
foreach ($sniffGroups as $sniffGroup) {
    $this->ensureIsAllInstanceOf($sniffGroup, Sniff::class);
}

// ...
private function ensureIsAllInstanceOf(array $objects, string $type)
{
    // ...
}
```

---

### 2. Do Not Use "else" Keyword
Why? Because it's useless. Because you don't need it and you never did either. The concept of this rule is early return, which employs the use of returning its value as soon as possible. Always work with a return

:x:

```php
// example 1
if ($status === self::DONE) {
    $this->finish();
} else {
    $this->advance();
}

// example 2
protected function index()
{
    if ($this->security->isGranted('ADMIN')) {
        $view = 'admin.pages.index';
    } else {
        $view = 'home.pages.access_denied';
    }
    
    return view($view);
}

// example 3
foreach ($members as $member) {
    if ($member->paid()) {
        $report[] = [$member->name => 'Paid'];
    } else {
        $report[] = [$member->name => 'Not Paid'];
    }
}

```

:+1:

```php
// example 1
if ($status === self::DONE) {
    $this->finish();
    return;
}

$this->advance();


// example 2
protected function index()
{
    if ($this->security->isGranted('ADMIN')) {
        return view('admin.pages.index');
    }
    
    return view('home.pages.access_denied');
}

// example 3
foreach ($members as $member) {
    if ($member->paid()) {
        $report[] = [$member->name => 'Paid'];
        continue;
    }
    $report[] = [$member->name => 'Not Paid'];
}

```
---

### 3. Wrap all primitives in classes

This rule says that you must encapsulate all primitive types (int, float, bool and string) within objects, thus preventing Primitive Obsession Anti-Pattern. This technique comes from an application of DDD (Domain-Driven Design) called Value Object, where we have a small value object, which will take care of a specific type of data.

:x:

```php
class Order
{
    public function notifyBuyer($email)
    {
        if (filter_var($email, FILTER_VALIDATE_EMAIL) === false) {
            throw new InvalidEmailException;
        }
        
        return $this->repository->sendEmail($email);
    }
}

```

:+1:

```php
class Email {

    public $email;
    
    public function __construct($email)
    {
        if (filter_var($email, FILTER_VALIDATE_EMAIL) === false) {
            throw new InvalidEmailException;
        }
        
        return $this->email = $email;
    }
}

class Order
{
    public function notifyBuyer($email)
    {
        return $this->repository->sendEmail(new Email($email));
    }
}

```

> WARNING: A potential problem with this approach is that it adds complexity to the codebase. In the translation of Object Calisthenics, it is stated that all primitive types must be involved in classes, however, we know that in PHP this can become unproductive and unnecessary, therefore, analyze how much that input or type can change, whether it needs validation, normalization, etc., only apply it if you have a real justification.


---

### 4. One dot per line

This “point” is what you use to call methods it would be a ->
It makes code easier to read and reinforces the Open-close principle. This rule is an example of the Law of Demeter: you should never use more than one object operator, that is, you should not chain method calls together.

:x:

```php
class Dog
{
  public function __construct(Breed $breed)
  {
    $this->breed = $breed;
  }
}
class Breed
{
  public function __construct(string $color)
  {
    $this->color = $color;
  }
}

$dogColor = $dog->breed->color;

```

:+1:

```php
class Dog
{
  public function __construct(Breed $breed)
  {
    $this->breed = $breed;
  }

  public function breedColor()
  {
    return $this->breed->color;
  }
}

$dogColor = $dog->breedColor();

```

> ATTENTION: There is an exception. It does not apply to Fluent Interfaces and anything that implements the Chaining Pattern (widely used, for example, in Query Builders).

---

### 5. Don't abbreviate

Why? Because it increases understanding of the context. Because it's bad and because I don't have to understand it. Abbreviations can be confusing and tend to hide larger problems. Analyzing why you are abbreviating is a great solution. Could this be happening because you are typing the same word multiple times? If true, perhaps you should reanalyze your code to remove the duplications. Another recurring case is when the names of methods or variables are long, this could be a sign that your class is doing things that don't belong there, that is, reviewing the Single Responsibility Principle.

:x:

```php
class EM
{
    // ...
}

```

:+1:

```php
class EntityMailer
{
    // ...
}
```

---

### 6. Keep all classes smaller

Keep in mind that it is recommended that a class has a maximum of 150 lines (PHP), and that packages have no more than 10 files. Generally, when we create a class with more than 150 lines, we assign it more responsibilities, making them more difficult to understand and also to reuse. Classes and packages must be cohesive and have a purpose, and that purpose must be easy to understand.

:x:

```php
class SimpleStartupController
{
    // 300 lines of code
}
```

:+1:

```php
class SimpleStartupController
{
    // 50 lines of code
}
```

:x:

```php
class SomeClass
{
    public function simpleLogic()
    {
        // 30 lines of code
    }
}
```

:+1:

```php
class SomeClass
{
    public function simpleLogic()
    {
        // 10 lines of code
    }
}
```

---

### 7. No classes with more than two instance variables.
Do not have more than two instance variables in your class. This is one of the most difficult rules to implement, as it depends on a completely different mindset than usual. By having a maximum of two instance variables, will ensure that we are once again respecting the Single Responsibility Principle and High Cohesion. If your class has more than two instance variables, it is very likely that it is carrying out more than one responsibility.

:x:

```php
class Student
{
  public $name;
  public $email;
  public $phone;
  public $address;
  public $city;
  public $country;
  public $courses;
  public $notes;
  ...
}

$student = new Student(
  "Tadeu Barbosa",
  "tadeufbarbosa@gmail.com",
  "+5531900000000",
  "...",
  "...",
  "...",
  "...",
  "..."
);

```

:+1:

```php
class Student
{
  public $person;
  public $address;
  public $courses;
}

$person = new Person(
  "Tadeu Barbosa",
  "tadeufbarbosa@gmail.com",
  "+5531900000000"
);
$address = new Address("Lorem Ipsum dolor", "..", "..");
$courses = new Courses([...], [...]);
$student = new Student($person, $address, $courses);
```
---

### 8. Don't Use Setters Or Getters.

Always remmeber that 
- Classes should not contain public properties.
- Method should [represent behavior](http://whitewashing.de/2012/08/22/building_an_object_model__no_setters_allowed.html), not set values.
  
At first it may seem like a very strange rule, however, the idea is very basic. You remove getters and setters to be able to add decisions to the object itself. Any decision based entirely on the state of an object must be made directly there. There are many benefits when we apply this idea. We reduce the duplication of rules and provide a better understanding of that object. We also enrich our object with more valuable and meaningful logic and methods, not just using it as a class with just data.

:x:

```php
class Buyer {

    protected $name;
    protected $purchases;
    
    public function getName() {/**/}
    public function setName($name) {/**/}
    
    public function getPurchases() {/**/}
    public function setPurchases($purchases) {/**/}
}

```

:+1:

```php
class Buyer {

    protected $name;
    protected $purchases;

    public function addNewPurchase()
    {
        $this->purchases++;
    }
}
```
---

## B. [Read PSR-2 Coding Style guide](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-2-coding-style-guide.md)

## C. [Read Clean Code & SOLID In PHP](https://github.com/piotrplenik/clean-code-php)
