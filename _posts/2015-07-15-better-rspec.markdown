---
title:  "Better RSpec"
date:   2015-07-15 9:00:00
description: Writing good test suites
---

What better way to start a programming blog than to write some good test suites. 

## 1. How to describe your methods
When I was learning how to write a test in [RSpec][rspec], like testing a simple method:

``` ruby
  def add_two_numbers(a, b)
    a + b
  end
```

I was doing it like:(BAD)

``` ruby
  describe "adding two numbers" do
    # ...
  end
```

When a straight-forward description is better.

``` ruby
  describe ".add_two_numbers" do
    # ...
  end
```

**Use "."(dot) when referring to a class method and "#" for instance method. Like:**

``` ruby
  describe '.authenticate' do
  describe '#admin?' do
```

## 2. Use let and let!
When you have to assign a variable, instead of using a before block to create an instance variable, use **let**. Using let, the variable lazy loads only when it is used the first time in the test and get cached until that specific test is finished. 

**BAD**:

```ruby
  describe "#category_id" do
    before { @product  = FactoryGirl.create(:product)}
    before { @category = Category.find(@product.category_id)}

    it 'sets the category_id' do
      expect(@product.category_id).to equal(@category.id)
    end
  end
```

**GOOD**:

```ruby
  describe "#category_id" do
    let(:product)  { FactoryGirl.create(:product)}
    let(:category) { Category.find(product.category_id)}

    it 'sets the category_id' do
      expect(product.category_id).to equal(category.id)
    end
  end
```

## 3. Use Factories

 **BAD**

```ruby
  let(:user) { User.create(name: 'Juan Dela Cruz', age: 21) }
```

 **GOOD**

```ruby
  let(:user) { FactoryGirl.create :user }
```
Learn more about [Factory Girl][factory_girl].

## 4. Use matchers
If you're using Rails, [thoughtbot][thoughtbot] created a wonderful gem called [shoulda_matchers][shoulda].
It lets you test associations, validations and more.

```ruby
  describe Person do
    it { should belong_to(:organization) }
  end

  describe Robot do
    it { should validate_presence_of(:arms) }
  end
```

## 5. Autorun test with [guard][guard]
I always use this gem. It watches your test files and automagically run your specs.
Check the repo for installation guide and setup.

[rspec]: http://rspec.info/
[factory_girl]: https://github.com/thoughtbot/factory_girl
[shoulda]: https://github.com/thoughtbot/shoulda-matchers
[thoughtbot]: https://robots.thoughtbot.com
[guard]: https://github.com/guard/guard-rspec
