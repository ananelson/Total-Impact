# The Template Plugin

## Introduction

The template plugin is a template to use for the preparation of your own Total-Impact plugins. You should replace the text as noted in this documentation, the plugin itself, and the various test scripts. This documentation is written using Dexy which means that the documents themselves will act as a test. If you run Dexy over your local repository and you have everything setup correctly then your version of this document should make sense

The python plugins for Total-Impact have a simple structure with three routines. The *run_plugin* method coordinates the action of the <em>get_data</em> and *parse_data* methods. The <em>main</em> method simply handles parameter passing from the rest of the Total-Impact system.

## Imports

The additional libraries required for this plugin are:

{{ d['template-plugin.py|idio']['imports'] }}

## The data source

Our plugin obtains data from the <em>data-source</em> using a <em>identifier</em> as the identifier. We are using <em>identifier</em> as the test identifier for this documentation.

{{ d['template-plugin.py|idio']['data-source'] }}

<!-- TODO show where the test code sets the test identifier -->

The data source returns a <em>page</em> in the following form when queried with our test identifer.

<!-- TODO show the result of running get_data with the default identifier -->

## Plugin specific methods

### run_plugin

In most cases this method will not need to be changed, feel free to remove this section if you haven't modified the run_plugin method

The run_plugin method coordinates the action of the other two core methods.  The first step is to check that the identifer is of the right type for this data source. The ID_PATTERN variable is set

<!-- TODO show where the regex for the ID_PATTERN variable is set -->

The method first checks that the <em>identifier</em> it has been passed matches the pattern specified</em>

<!-- TODO show the check for the id pattern matching -->

The method then obtains the page as specified by calling the <em>get_data</em> method. If a page is correctly received it then parses it using the <em>get_stats</em> method and returns the response to Total-Impact core.

<!-- TODO show rest of run_plugin method -->

The form of the returned dictionary for this plugin is as follows.

<!-- TODO show the result of running run_plugin with default id -->
<!-- TODO need to write script? -->

### get_data

In most cases this method will not need to be changed, feel free to remove this section if you haven't modified the get_data method. The only place likely to require change is the fetching of the page itself which might require encoding or some preprocessing or a more complex call

The get_data method first checks that an id has been passed to it and if not it returns <em>None</em>.

<!-- TODO show checking of id -->

The query URL is set by combining the BASE_DATA_URL with the id and an attempt is made to obtain the page. If successful the page is returned. If a 404 is received then the routine returns <em>None</em>. If there is some other error this is raised back up the request chain.

<!-- TODO show the remainder of get_data method -->

If functioning correctly the get_data function should return a <em>page</em> of the form shown here.

<!-- TODO show the page returned - need to write script separately to do this? -->

### get_stats

This is the core specific method of your plugin and should be clearly documented as others will likely wish to build on it. The description for the template method is necessarily a little vague.

The get_stats routine receives the raw (unless you've done some upstream processing) page returned by get_data. The parsing will be specific to the specific plugin and data source.

The method first checks that the page has been provided and if not it returns *None*.

<!-- TODO show section checking that page is available -->

The actual parsing routine is wrapped in a try clause in case of parsing problems.

<!-- TODO show the parsing section -->

If you wish to divide up your description of the parsing component of your plugin you can easily add more sections by adding additonal ### @export markers to your code

The response to be sent to the total impact core is then wrapped as a Python Dictionary/JSON object and returned.

<!-- TODO show the section that sets up the dictionary -->

The results are returned as a dictionary in the following form:
<!-- TODO show what the method returns given the default id - need to write script? -->

### main

There should not be any need to change main. This is included only for completeness sake and can be removed if you haven't modified main within your plugin.

The main method accepts a command line argument from the Total-Impact core and parses the arguments. As all plugins work to obtain data based on one identifier from one data source this should only ever be called with one argument which is checked. The run_plugin method is then called and the final response returned back to the command line where it is collected.

{{ d['template-plugin.py|idio']['main'] }}
