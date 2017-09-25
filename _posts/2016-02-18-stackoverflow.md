---
layout: post
title: "Find answers in stackoverflow"
description: "stackoverflow"
categories: find
tags: [maven]
---

#### [Difference @Controller and @RestController annotation](http://stackoverflow.com/questions/25242321/difference-between-spring-controller-and-restcontroller-annotation)

  - @Controller is used to mark classes as Spring MVC Controller.
  - @RestController is a convenience annotation that does nothing more than adding the @Controller and @ResponseBody annotations (see: Javadoc)

~~~
@Controller
@ResponseBody
public class MyController { }

@RestController
public class MyRestController { }
~~~


#### [Using Spring 3 autowire in a standalone Java application](http://stackoverflow.com/questions/3659720/using-spring-3-autowire-in-a-standalone-java-application)

~~~
@Component
public class Main {

    public static void main(String[] args) {
        ApplicationContext context =
            new ClassPathXmlApplicationContext("META-INF/config.xml");

        Main p = context.getBean(Main.class);
        p.start(args);
    }

    @Autowired
    private MyBean myBean;
    private void start(String[] args) {
        System.out.println("my beans method: " + myBean.getStr());
    }
}

@Service
public class MyBean {
    public String getStr() {
        return "string";
    }
}
~~~


---


#### [Perhaps you are running on a JRE rather than a JDK](http://stackoverflow.com/questions/19655184/no-compiler-is-provided-in-this-environment-perhaps-you-are-running-on-a-jre-ra)
- Go into Window > Preferences > Java > Installed JREs > and check your installed JREs. You should have an entry with a JDK there. Select the Execution Env as show below. Click OK
Then RightClick Project -> Maven -> Update Project
- ![](/images/yBB7s.png)

---

#### [Runtime vs Compile time ](http://stackoverflow.com/questions/846103/runtime-vs-compile-time)
The difference between compile time and run time is an example of what pointy-headed theorists call the phase distinction. It is one of the hardest concepts to learn, especially for people without much background in programming languages. To approach this problem, I find it helpful to ask

  - What invariants does the program satisfy?
  - What can go wrong in this phase?
  - If the phase succeeds, what are the postconditions (what do we know)?
  - What are the inputs and outputs, if any?

#### Compile time

  - The program need not satisfy any invariants. In fact, it needn't be a well-formed program at all. You could feed this HTML to the compiler and watch it barf...
  - What can go wrong at compile time:
    - Syntax errors
    - Typechecking errors
    - (Rarely) compiler crashes
  - If the compiler succeeds, what do we know?
    - The program was well formed---a meaningful program in whatever language.
    - It's possible to start running the program. (The program might fail immediately, but at least we can try.)
  - What are the inputs and outputs?
    - Input was the program being compiled, plus any header files, interfaces, libraries, or other voodoo that it needed to import in order to get compiled.
    - Output is hopefully assembly code or relocatable object code or even an executable program. Or if something goes wrong, output is a bunch of error messages.

#### Run time
  - We know nothing about the program's invariants---they are whatever the programmer put in. Run-time invariants are rarely enforced by the compiler alone; it needs help from the programmer.
  - What can go wrong are run-time errors:
    - Division by zero
    - Deferencing a null pointer
    - Running out of memory
  - Also there can be errors that are detected by the program itself:
    - Trying to open a file that isn't there
    - Trying find a web page and discovering that analleged URL is not well formed
  - If run-time succeeds, the program finishes (or keeps going) without crashing.
  - Inputs and outputs are entirely up to the programmer. Files, windows on the screen, network packets, jobs sent to the printer, you name it. If the program launches missiles, that's an output, and it happens only at run time :-)
