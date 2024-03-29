![](/galleries/2010-10-08-cplusplus-behaviour-driven-development-tools/-behaviour-driven-clarity.jpg)
C++ is still considered one of the most powerful and flexible tools for making fast software, especially where other systems like Python, Java or Ruby are not available.

Behaviour Driven Development is a current practice in programming that is changing the way coders are thinking. It is bringing testing, coding and design closer together. The theory is that things get done right and work sooner, instead of nearly working, not quite what anybody wanted, and having very little to measure against.

One way to implement this is as a set of Behaviour specifications, such as the type built with the tool Rspec. The specs grow as functionality is scheduled to be introduced to a product. This specification can be run against the code, show where it is deficient. When other features or changes are added, running the spec can quickly highlight a regression. A regression caught as it was created should be relatively easy to find. A regression caught a few months later in end-of-product testing will be harder to fix, when there is nearly no time left to fix it.

So Behaviour Driven Development is about quality. It is also about the confidence that the code does what it should. BDD is about clear communication about what code should be doing so that the tester, coder and designer are all talking in the same language.

C++ is currently less refined in this realm than Ruby or Java, but it is catching up. Tools for BDD are being created. They probably need to borrow a little from each other. They need support from the C++, BDD and Test Driven Development communities to flourish. They will need to be linked up with CI systems like Hudson or Cruise Control to really fly. However, even embryonic systems like CppSpec and Igloo can give value to a product.
<hr>
What is behaviour driven development (BDD)? It is a method for developing software where the behaviour of a bit of code, or an app, is described first, in a formal but as plain English as possible. This description or specification actually forms an executable set of tests against the software, so initially, they would fail. Later, as the software is built by programmers, these will start to pass. If the software needs to be refactored, then it would be assumed that these specifications of behaviour should still pass. If a new team member needs to understand what some code should do, they need only look at this specification to see. Then for them to know how much of the spec it does, they can run this specification and see the result.

BDD has evolved from a few disciplines in software practice. Those include unit testing evolving into TDD (Test Driven Development), and the automation of many tests. It comes from bringing testers, and product designers back in close to development teams and encouraging these team members to start speaking the same language, by keeping the words as plain as possible. In terms of automation, BDD frameworks fit into CI frameworks so the set of specifications can be run on code regularly, a team can then see feedback on their progress, and quickly be aware of any regressions. For a developer, running the specs on their own desk gives them a quick scaffold to build their code. For a developer to start thinking and writing specs, in plain English and using the right words - like "This thing should say hello," it both closes communication gaps between them and the rest of the team, and means that the code itself starts to be more readable and maintainable.

This article is not intended to evangelise BDD, TDD or testing in general. It is designed so I can share my experiences on them with C++ (I've used them plenty with Python and Ruby [RSpec](http://rspec.info/) and [Jasmine for JS](http://pivotal.github.com/jasmine/) for JS, and built an AS2 BDD framework), where the frameworks to facilitate this are a little less well developed. It is also a call to action for those with interests in this realm. Perhaps for developers to combine BDD efforts for a great result. It is a mention of where they could improve and includes tutorials for developers to get in there and actually try building examples with them so they can start being used.

# Getting the Words Right

![](/galleries/2010-10-08-cplusplus-behaviour-driven-development-tools/-bdd-getting-the-words-right.jpg)

A critical concept in a Behaviour Driven Design framework is [getting the words right](https://behaviourdriven.org/GettingTheWordsRight "GettingTheWordsRight - Behaviour-Driven Development"). BDD frameworks offer a DSL (Domain Specific Language) in the language you are using, which can express the specifications in a way where the programming language almost gets out of the way and lets users say what they mean. There is always going to be language-specific syntax to get around, but the better the DSL has been put together, the less this syntax will get in the way and the more it will flow.

So here is an example describing a bit of code using [Jasmine](https://jasmine.github.io "Jasmine: BDD for Javascript | Jasmine") - a very well developed and supported BDD framework for Javascript.

    require "calendar"

    describe Calendar, "finding first gap" do
        include CalendarHelperMethods
        
        it "Should find the the first gap in the calendar longer than 30 minutes" do
            cal = Calendar.new()
            addTestEvents(cal)
            cal.firstGap(:withSize=>30.minutes).should == gapList[0].startTime
        end
    end

This is a (very!) abridged snippet of a set of specs, which I will add for download and some code that they run with for readers to look at, although the focus here is on the C++.
Quickly describing what this does, it is a specification to describe how a user of a calendar would find the first gap, and what this function should do. Somebody wants to find a gap in their calendar of 30 minutes or more.
It includes a set of helper methods to cut down on the boilerplate needed for testing and leave the developer less to repeat. In the one specification this description holds, a calendar object is instantiated (Ruby people will spot that this double bracket is superfluous and unnecessary). A helper method "addTestEvents" sets up a given and known set of events, and the same helper provides a gapList, a list of the gaps, by start time and duration.
The actual expectation here is pretty clear. When firstGap has been called, with a parameter specifying that the gap should have a size of 30 minutes, it should return a start time equal to the first listed gap. - since the helper provided a set of events and gaps.
In other words:
* Given a known set of events
* Ask for the Calendars First Gap with a size of 30 minutes
* It should return a start time equal to the start time of the first gap in the list

Here, the ruby syntax adds things like ".should" instead of simply " should," and should equal becomes ".should ==" (there is an equal but it compares object identities instead of content, not useful for our purposes).

# Actual tools for C++ BDD and Specification

There is one heavyweight tool that can do C++ testing, [FitNesse](http://fitnesse.org/). I've not spent time on it here, as getting some lightweight tools on the go and well developed will hopefully give faster gains to somebody looking to employ these methods. FitNesse requires a bit more investment in infrastructure, time and set up than the other tools. Fitness also needs a bit more in the way of code preparation than the other frameworks.

Next up is [CppSpec](https://github.com/tpuronen/cppspec). I will get plenty of detail later, but in short, it is a relatively lightweight BDD tool for C++ that is based on the Boost library and needs to be downloaded as source then built using Cmake. It is a project that is very much alive with quite a responsive developer on it. There are plenty of features for matchers and expectations, however, as we will see, some of the boilerplate needed to get it moving could do with reduction.

Also great is [Igloo](https://iglootesting.wordpress.com "Igloo - BDD Style Unit Testing for C++"). This is a purely header-based library, with no other dependencies, making it somewhat easier to fit into a project than CppSpec. It has some nice features around keeping spec declarations simple. However, it lacks one or two features in its matchers.

I see some similar tools, different efforts to build a decent C++ spec tool. I've been looking at these two, and see they both have some real strengths, and a couple of weaknesses, but I think pooling resources could really get something great.

# Screencast -- using Igloo in XCode

I've made a screencast showing how Igloo can be used to test things in C++ and using the XCode environment. As Igloo is a header-only setup, it is not difficult to integrate into any tool, Visual Studio, Makefiles, CMake, Boost Build (BJam) etc...

http://www.youtube.com/watch?v=cV4jzIjD754

# Hold on - Whats a DSL?

A DSL is a Domain Specific Language. It is a way of using more plain English, or at least Jargon specific to a domain to program or script. This is easier to use than the usual jargon and syntax laden native constructs. Constructing a good DSL leads to more self-documenting and easy to understand code, where the intent is stated clearly and not obfuscated by syntax and subscripts. In the case of BDD, consider these examples:

    Test(a,2);
    Expect.that(a, Equals(2));

The second one is longer but definitely states precisely what was intended here. It certainly means that a developer can read the code and should be able to gather what is going on. Another example:

    Test(duration, 1800);
    Expect.that(duration, Equals(60, minutes));

In the first case here, 1800 could be replaced with 60 * 30 perhaps, but either way, it is still unclear. The second example is again stating its intent plainly.

A DSL can be brought into a development environment in one of two ways. The first type is an "External DSL," based on building a parser with its own lexicon, grammar and interpreter. This would mean getting to know things like Lexx and Yacc and divorces that DSL from the power of a fully-fledged language. Word to the wise, if you've done this before, you'll know that being able to import a well-known interpreter like Python or Ruby will get a lot more done than trying to build that from scratch.

The alternative way, and IMHO better, is an internal DSL, building it into the language you are using. This is ideal for tests, as you can use constructs that belong to your language, thus being in familiar territory. It picks up more of your language's natural syntactic noise. It may mean some interesting problems to be solved in libraries to make that grammar work, but the results can be impressive. Both Igloo and CppSpec are using an internal DSL style to get their results.

[More information on DSL](http://en.wikipedia.org/wiki/Domain-specific_language "Domain-specific language - Wikipedia, the free encyclopedia")

# Documentation for Igloo and CppSpec

The two frameworks mentioned, Igloo and CppSpec are both early-ish projects. Their documentation and library maturity is currently in the early stages, and they need some community usage and support to really get them going. Getting them into more developers projects, running in Hudson and some of their pain felt, and boilerplate smashed further into simpler reusable DSL macro's will serve to improve them. I also recommend their users get to know either a little ruby and rspec or a little JS and jasmine - because this gives an idea of how pleasing a BDD DSL can be.

I am also cooking up screencasts for some example projects to get people rolling with either.

Documentation Resources for CppSpec:
[CppSpec Examples](http://github.com/tpuronen/cppspec/tree/master/examples/ "examples at master from tpuronen - cppspec - GitHub")

Documentation For Igloo
[Creating a Test Application](https://iglootesting.wordpress.com/documentation/test-application-basics/ "Igloo - BDD Style Unit Testing for C++")

# Igloo, meet CppSpec, and CppSpec meet Igloo

## Why they should perhaps link up, combine forces and code for something truly awesome.

CppSpec and Igloo look like they are aiming at a very similar goal, while FitNesse is in a league of its own. These lightweight tools, however, have real potential to bounce ideas from each other.

As I have mentioned, a great model (IMHO) for BDD tools is probably RSpec - it kind of flows nicely. A DSL in C++ may not be quite as cute as that, but it can be not far off. Another inspiration for great spec tools is Jasmine, from the Javascript world - which is getting closer to what a C++ spec may look like.

Igloo and CppSpec are the closest I see to rspec and Jasmine. But here's where joined efforts could really close this gap beautifully.

Igloo has as its first strength being a header-only library - which is pretty handy, while CppSpec requires boost and compilation with CMake. Perhaps some greater automation of getting this running would be helpful, although the support from the developer was second to none.

Igloo has got the simplest DSL for actually declaring Specs. I would probably map Context to "Describe" and "Spec" to "It" to bring it closer to the rspec/Jasmine world. CppSpec currently needs a lot of boilerplate to build specs and fixtures, with template instantiation and then registration functions being typed out in each spec file.

They have relatively like-for-like richness in their matcher DSL - comparing them:

CppSpec:
    
    specify(myValue, should.equal("Hello"));
    
Igloo:

    Assert::That(myValue, Is().EqualTo("Hello"));

Declaring a spec in with Igloo:

    Context(describeHello) {
        Spec(getGreetingShouldReturnHello) {
            Hello hello; //make instance of class "hello" under test
            Assert::That(hello.getGreeting(), Equals("Hello"));
        }
    };

Declaring the same spec in CppSpec:


    class DescribeHello : public CppSpec::Specification<Hello, DescribeHello> {
    public:
        DescribeHello() {
            REGISTER_BEHAVIOUR(DescribeHello, getGreetingShouldReturnHello);
        }

        void getGreetingShouldReturnHello() {
            specify(context().getGreeting(), should.equal("Hello"));
        }
    } describeHello;

Clearly, Igloo has the more condensed syntax, albeit with more implied framework magic.

However, where CppSpec really shines is it can run/invoke a function and expect exceptions, something missing from Igloo (unless I just haven't found it yet). CppSpec has more of an extensible matcher system compared with Igloo.

Taken straight from the CppSpec examples:

    specify(invoking(&Stack<int>::pop).should.raise.exception<std::exception>());

Igloo also does not catch exceptions in its specs, letting them bubble up to the top, it really could be more helpful if it was to capture them, and specify which spec they were thrown in.
If the reduced boilerplate around declaring specs and fluency from Igloo, could be combined with the exception matching of CppSpec, then this may be a significant step towards having very easy to use Cpp tools for BDD.

Packages or simpler installers for CppSpec would make it easier to put in a C++ project (ah - were there something like Maven for a C++ project and its dependencies).

# Extending Igloo to expect exceptions

Because a project I am working on required this, and I noted it's lack in Igloo, I created a small header-only helper that expects an exception to have been thrown. I will not claim it is perfect, only that it is good enough.

It can be downloaded from GitHub at: (https://github.com/dannystaple/igloo/blob/helpers/igloo/igloo_helper.h)- I've made a pull request so the original author can consider it.

What do you get?

    /*
        Checks that an exception was thrown. Doesn't care what.
        @param block A block of code that should throw an exception
        
        For use inside an Igloo Spec
    */
    #define ShouldThrowError(block)

When passed in a block of code, this will fail an internal Igloo expect if that code did *not* throw an exception. It is promiscuous in that any exception will do. To use it, download it, and add the header to the top of your Spec code:

    #include "IglooHelper.hpp"

Where it is needed for part of your spec:

    Spec(shouldRejectOversizeMinutes) {
        ShouldThrowError({ DateTime dt("08:70"); });
    }

The other macro that can be used here is ShouldThrowWhatError, which is more selective in that an exception derived from std::exception, which matches a given "what" should have been fired:

    /*
        Checks that an exception was thrown, with a given "what" value.
        @param block A block of code that should throw an exception
        @param expected_what A string to compare the what field of the error with.
        
    For use inside an Igloo Spec.
    */
    #define ShouldThrowWhatError(block, expected_what)

The usage, as above starts with including the same header. Then when using in your spec:

    Spec(shouldRejectANonTimeString) {
        ShouldThrowWhatError({ DateTime dt("foobar"); }, "Invalid datetime");
        ShouldThrowWhatError({ DateTime dt("08:45:55"); }, "Invalid datetime");
    }

This means that another exception fired will either not be caught at all (and bubble up), or if it is a std::exception derivative, it will fail on not being equal to the expected what.

# Mocking or Faking

Mocking is a technique used in TDD and BDD to provide fake versions of objects that the code under test is expected to interact with.
This can firstly be used to avoid the code interacting with real database writes or drivers and similar. This means that the code can be better isolated.

Secondly, the fakes/mocks can be spied on to ensure that the interface was used in a certain way.

Fakes are to be used carefully, as while they can help, if they are overdone, you may end up with tests that are too fragile.

Currently, I am still yet to research what provision there is for these in C++. Neither Igloo nor CppSpec are that far forward with this, however, [Googlemock](https://github.com/google/googletest/tree/master/googlemock) might well be usable with this. This brings me to wondering how advanced a Mocking + BDD framework built on the concepts of GoogleTest and GoogleMock might be and if those two projects could be used to "bootstrap" a more advanced C++ BDD testing setup?

Also now there is [http://sourceforge.net/projects/turtle/](Turtle) - a C++ mocking library based on the Boost framework, that may also have a real candidate for the de-facto mocking library for Boost. I am yet to play with this to see how powerful it is.

# The other BDD for C++

There is another BDD - Binary Decision Diagrams - which has tools like BuDDy. This is an entirely different use of the acronym and is not the same as Behaviour Driven Development. I am not sure which of these acronyms have precedent, but if you were looking for information on the other kind of BDD please try this:
[BuDDy - BDD C++ Package](http://buddy.sourceforge.net/manual/main.html), related to JBDD and CUDD.

# Background reading: Behaviour Driven

<iframe style="width:120px;height:240px;" marginwidth="0" marginheight="0" scrolling="no" frameborder="0" src="//ws-eu.amazon-adsystem.com/widgets/q?ServiceVersion=20070822&OneJS=1&Operation=GetAdHtml&MarketPlace=GB&source=ss&ref=as_ss_li_til&ad_type=product_link&tracking_id=orionrobots-21&language=en_GB&marketplace=amazon&region=GB&placement=1934356379&asins=1934356379&linkId=de50d4cafa99a2641b6ed309e9cd5cbe&show_border=true&link_opens_in_new_window=true"></iframe>

There are few books on this topic as it is currently still a very new branch of computing. However, this book is a useful reference, it shows some of the best tools and pulls some of the heavyweight contributors to this methodology, notably including Dan North.
