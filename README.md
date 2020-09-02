# frontend-template-resources

Simple templates.

I've split them into two distinct directories:

* Jinja2 - the python templating language (or more accurately, a template language that supports python syntax and can be easily rendered by python libraries). Used by the gssutils TransformTracer.render() method.
* Handlebars - standard all-purpose Javascript based templating language. 

# Use with the gssutils trace.render() method

_Note: Arguably the wrong place for this, but inside gssutils seems wrong too._

Any template from this repos `/templates/jinja2` can be passed directly into the gssutils `trace.render()` method without needing a full url.

Example: `trace.render("spec_v1.html")`

The trace.render method also supports the passing in of full urls (i.e jinja2 templates in other locations).

### Additional Keywords

You can pass the following additional keywords to `trace.render()`.

`output=<string>`: the directory to write the rendered html file to.

`foreign_sources=<dictionary>`: pass in additional urls for json data sources, for use with more complicated templates. 

Complex usage example:

```python
# We want the template to have access to some cmd json data, accessible in the template as 'cmd'
# We also want to output the rendered html to ./my-directory/child
fs = {
    "cmd": "https://api.beta.ons.gov.uk/v1/datasets/ashe-tables-7-and-8/editions/2014"
}
trace.render("spec_v1.html", output="./my-directory/child", foreign_sources=fs)
```

Note, by default `trace.render()` has access to the following data (any foriegn_sources are addional, not instead of):

* info_json: a dictionary/hashmap of a pipelines info.json file.
* raw_data: the information captured by the tracer during runtime.

I've included examples of both in `/example_sources`.





