##webmin-notes

A small module that allows you to create/edit/remove notes.

![Image of module](http://i.imgur.com/Yfa6rDI.png)

![Image of module](http://i.imgur.com/R1pTHFp.png)

![Image of module](http://i.imgur.com/H7GItww.png)


###Available note-methods:###

| Method        | Value           
| ------------- |:-------------:
| status      	| 0 = disabled / 1 = enabled
| style      	| warning, info, danger, success
| title      	| note-title
| content      	| note-content


###Usage###
Add the following in your template file (body.cgi or index.cgi):

```perl
&foreign_require("webmin-notes");
@notes = &webmin_notes::list_notes();
foreach my $n (@notes) {
	#now you have access to each note
	#Available methods: status, style, title, content
}
```


###Example:###
```perl
#This example fits @winfuture Bootstrap theme (http://theme.winfuture.it/)

&foreign_require("webmin-notes");
@notes = &webmin_notes::list_notes();
foreach my $n (@notes) {
	if ($n->{'status'} == 1) {
		print '<div class="alert alert-'. html_escape($n->{'style'}) .'" role="alert"><b>'. html_escape($n->{'title'}) .'</b> '. html_escape($n->{'content'}) . "</div>\n";
	}
}
```