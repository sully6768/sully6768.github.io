---
layout: post
title: What's New in JBoss Fuse 6.3
---

JBoss Fuse 6.3 released recently and contains a number of updates.  They include:

* New versions included for Apache Camel (2.17), Apache CXF (3.1), and Jetty (9)
* New components including Kubernetes, Slack, ServiceNow, Apache Spark, PDF and Paho.

Over the next month or so I will be stepping through a number of the updates to give you an idea of what the impacts are of each addition are.

So where to start...

Tooling
----------------

IMHO probably one of the biggest improvements, from a developers perspective, are the tooling updates for the Fuse IDE.  To start with JBoss Fuse IDE  get a greatly improved graphical diagram editor 

Tooling Install
----------------

It might be easier to go through and get hands on to give you a better idea of how much its improved.

To start with lets get it installed. For the hands on portion I will be using the JBoss Developer Studio 9.x environment which is based on Eclipse.

To install the tooling for JBoss Fuse open the Red Hat Central screen which can be accessed by clicking the Red Hat logo on the tool bar:

![Red Hat Central Button]({{ site.baseurl }}/images/20161107/toolbar-rhcentral-pointer.png)

When the screen appears, click the Software/Update tab at the bottom of the screen:

![Red Hat Central Button]({{ site.baseurl }}/images/20161107/rhc-screen.png)

Finally, select the JBoss Fuse Development tools from the list of available installations. 

> **Note:** There is currently an issue if you have both the JBoss Fuse and Spring IDE tools both installed in the IDE. The Spring IDE tooling will cause new Fuse projects to ignore the Camel project facets and you will miss out on the design tools.


![Red Hat Central Button]({{ site.baseurl }}/images/20161107/rhc-fuse-tools-install.png)



### Rest DSL Code

{% highlight java linenos %}
protected RouteBuilder createRouteBuilder() throws Exception {
    return new RouteBuilder() {
        @Override
        public void configure() throws Exception {
            rest("/say")
                .get("/hello").to("direct:hello")
                .get("/bye").consumes("application/json").to("direct:bye")
                .post("/bye").to("mock:update");
 
            from("direct:hello")
                .transform().constant("Hello World");
            from("direct:bye")
                .transform().constant("Bye World");
        }
    };
}
{% endhighlight %}

The easiest way to make your first post is to edit this one. Go into /_posts/ and update the Hello World markdown file. For more instructions head over to the [Jekyll Now repository](https://github.com/barryclark/jekyll-now) on GitHub.
