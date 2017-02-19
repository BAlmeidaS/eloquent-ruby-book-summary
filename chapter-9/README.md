# Specs
## Test::Unit
Test::Unit comes with Ruby itself and is a member of XUnit family of testing frameworks.

By the way, MiniTest is a complete rewrite of Test::Unit

each test is packaged in a method whose name need to begin with **test_**

```
def test_document_holds_content
  text = "the content"
  doc = Document.new "the content"
  assert_equal text, doc.content
end
```

Test must have nice descriptive name.

The Test class must be a subclass of Test::Unit::TestCase

```
require 'test/unit'
require 'document.rb'

class DocumentTest < Test::Unit::TestCase
  def test_document_holds_content
    text = "the content"
    doc = Document.new "the content"
    assert_equal text, doc.content
  end
  
  def test_that_doc_can_return_words_in_array
    text = "some words"
    doc = Document.new text
    assert doc.words.include?("some")
    assert doc.words.include?("words")    
  end
end
```
running tests: `$ruby document_test.rb`

#### setup
you can create the setup method: `def setup; end`

The setup method gets called before each test method is run

#### teardown
you can create the teardown method: `def teardown; end`

The teardown method gets called after each test method gets run.

### asserts
`assert` `assert_equal` `assert_not_equal` `assert_nil` `assert_not_nil`

`assert_match /time.*/, "it is time to rumble"`

`assert_instance_of String, "hello world"`

`assert_raise ZeroDivisionError { x = 1/0 }`

`assert_raise ZeroDivisionError { x = 1/2 }`

## RSpec
Don't test it, spec it.

obs: The following code, inspired by the book, contains an old syntax of rspec, but still worth learning.

tests should be read more like this:

"About the Document class; when you have a document instance, it should hang onto the text that you give it. It should also return an array containing each word in the document when you call the words method"


*rspec version:*

```
describe Document do
  before do
    text = "some words"
    doc = Document.new text
  end
  
  it "should hold on to the contents" do
    doc.content.should match(/some words/)    
  end
  
  it "should return all of the words in the document" do
    doc.words.should include("some")
    doc.words.should include("some")
  end 
end
```

The code above is not a test, it is a description.

running tests: `$spec <<class_name>>_spec.rb`

#### before and after

As `setup` Test::Unit, RSpec contains:

```
before do
  #create_setup
end
```

As `teardown` Test::Unit, RSpec contains:

```
before do
  #do_something
end
```

## Stubs
A stub is an object that implements the same interface as one of the supporting cast members, but returns canned answers when its methods are called.

supose that that we have a class, `PrintableDocument`, that implements method `print`, which receive some `printer`. `printer` has to implement two methods, `available?` and `render`:

```
class PrintableDocument < Document
  def print(printer)
    return "unavailable" unless printer.available?
    printer.render "#the Title #{title}"
    printer.render "#the author is #{author}"
  end
end
```

The question is, how do we test the print method without having to get involved with a real printer?. Create a stub printer.

```
describe PrintableDocument do
  before do
    text = "some words"
    doc = PrintableDocument.new text
  end
  
  it "should know how to print itself" do
    stub_printer = stub :available? => true, :render => "Done"
    doc.print(stub_printer).should == "Done"    
  end
  
  it "should return the proper string if printer is offline" do
    stub_printer = stub :available? => false, :render => "Done"
    doc.print(stub_printer).should == "unavailable"
  end 
end
```

## Mock
A mock is a stub with an attitude. Along with knowing what canned responses to return, a mock also knows which methods should be called and with what arguments.

While a stub is there purely to get the test to work, a mock is an active participant in the test, wathing how it is treated and failing the test if it does not like what it sees.

```
  it "should know how to print itself" do
    mock_printer = mock('Printer')
    mock_printer.should_receive(:available?).and_return(true)
    mock_printer.should_receive(:render).exactle(2).times
    doc.print(mock_printer).should == "Done"
  end
```

## Some considerations
Unit tests should run quick with the setup that every developer has, if if they take long time, none developer will run it. *they are your first line of defense, and in order to be any good they must be run often.*

Tests need to be independent of one another.

Make sure that your tests will actually fail. 

In the end, the point of Russ Olsen is simple, we don't care if you will practice the TDD or BDD, write test at the beginning or at the end, but write the tests!!!  