---
layout: post
title:  "Selenium Tutorial"
date:   2018-04-19 21:04:15 -0400
categories: selenium tutorial
---
## What is [Selenium](https://www.seleniumhq.org/)?
Selenium is a handy tool to automate browser testing. It's popularly used as a testing framework, but can also be used to automate many web browser functions.

## Tutorial

### Assumptions
* An internet connection
* Using a Mac
* Homebrew for ease of installing geckodriver
* Familiar / comfortable with Java
* [IntelliJ](https://www.jetbrains.com/idea/download/) IDE installed
* Knowledge of the JUnit testing framework

### Create a new IntelliJ Project
Let's create a new Java project. We won't need any special plugins, a plain project will do. We'll call it _SeleniumBasics_.
![IntelliJ Project Creation]({{ "/assets/IntelliJ_Project_Creation.png" | absolute_url }})

### Add Webdrivers to Our Project
We need to add the webdriver framework to our IntelliJ project. This allows us to use the provided code and API to test websites.

To simplify this tutorial, let's use Maven to retrieve all of the necessary libraries.

In IntelliJ go to File => Project Structure... => Libraries => + => From Maven...
![Add Dependencies]({{ "/assets/Add_Dependencies.png" | absolute_url }})

You should wind up with a window looking like the above. From here we want to search for _selenium-server_ and install the latest version (3.11.0 at the time of this writing). Continue on clicking _OK_ or _Apply_ as needed. Adding the dependencies this way also takes care of installing all of the drivers that we'll want / need.

### Create a New Java Class
![WebsiteTest]({{ "/assets/WebsiteTest.png" | absolute_url }})

Create a new Java class, _WebsiteTest.java_ inside the src directory of your project.

### Creating Our First Test
We'll now want to set this class file to be used for tests. While your cursor is over the class name, type _Option + Enter_ and select _Create Test_.

![OptionEnter]({{ "/assets/Option_Enter.png" | absolute_url }})

Follow the prompts and we'll wind up with a menu to configure the test class.

![CreateTest]({{ "/assets/CreateTest.png" | absolute_url }})

As can be seen, we don't have the JUnit5 module installed for our project. Click the _Fix_ button to install it, and follow all prompts. Change the class name to match ours (_WebsiteTest_) and click _OK_ for all prompts.

### Install geckodriver
From a command line type _brew install geckodriver_. This will install and place geckodriver on your PATH. We need this so we can run tests using the _FirefoxDriver_.

### Our First Test
{% highlight java %}
import org.junit.Test;
import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.firefox.FirefoxDriver;

import static org.junit.Assert.assertTrue;

public class WebsiteTest {

  @Test
  public void jkGyTest() {
    WebDriver driver = new FirefoxDriver();
    driver.get("https://jk.gy");
    WebElement header = driver.findElement(By.className("header"));
    assertTrue(header.isDisplayed());
  }

}
{% endhighlight %}

For this basic test, we're going to assert that an element with the class _header_ appears on my [personal page](https://jk.gy). As an aside, we may need to add JUnit4 to our classpath. IntelliJ is [wicked smaht](https://www.youtube.com/watch?v=DyF0tR6cQA4) and will do most of this for you. By typing _Option + Enter_ on any piece of code that is causing an error, IntelliJ should suggest some ways to fix it.

In layman's terms we've:
* Initialized a Firefox browser
* Accessed the my personal website
* Retreived an element from the webpage by class name (_header_)
* Verified that it is in fact visible on the page