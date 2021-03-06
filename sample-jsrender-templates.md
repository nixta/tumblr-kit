Sample JsRender Templates
=========================

The sample templates in this file use Boris Moore’s JsRender templating syntax (see the [demos and documentation](http://borismoore.github.com/jsrender/demos/) for more information).

These templates should be treated as a starting point only. Modify them to match the markup in your theme, and refer to Tumblr’s [API documentation](http://www.tumblr.com/docs/en/api/v2#text-posts) for details of the exposed object hierarchy for each post type.

Note that by its nature the [demo](http://dropbox.com/u/25640/tumblr-kit/demo/index.html) probably loads the same post into multiple containers, thereby making the post IDs non-unique. Avoid doing this if you want to make use of those for any reason.

### Audio post

```html
	<script id="tmpl-audio" type="text/x-jsrender">
		<article id="post-{{:id}}" class="post-{{:type}}">
			{{if track_name || artist || album}}
				<h1>{{:track_name}}
					{{if artist}} by {{:artist}}{{/if}}
					{{if album}} from ‘{{:album}}’
						{{if year}}({{:year}}){{/if}}
					{{/if}}
				</h1>
			{{/if}}
			{{:~getTintedAudioPlayer(#view, "#DDDDDD")}}
			{{if plays}}<p>{{:plays}} plays</p>{{/if}}
			{{:source}}
			{{for #data tmpl="#tmpl-metadata"/}}
		</article>
	</script>
```

### Chat post

```html
	<script id="tmpl-chat" type="text/x-jsrender">
		<article id="post-{{:id}}" class="post-{{:type}}">
			<h1>{{:title}}</h1>
			{{if dialogue}}
				<ul class="chat">
					{{for dialogue}}<li><strong>{{:label}}</strong> {{:phrase}}</li>{{/for}}
				</ul>
			{{/if}}
			{{for #data tmpl="#tmpl-metadata"/}}
		</article>
	</script>
```

### Link post

```html
	<script id="tmpl-link" type="text/x-jsrender">
		<article id="post-{{:id}}" class="post-{{:type}}">
			<h1><a href="{{:url}}">{{:title}}</a></h1>
			{{:description}}
			{{for #data tmpl="#tmpl-metadata"/}}
		</article>
	</script>
```

### Photo / Photoset post

```html
	<script id="tmpl-photo" type="text/x-jsrender">
		<article id="post-{{:id}}" class="post-{{:type}}">
			{{if photoset_layout}}
				<ul class="photoset">
					{{for photos}}<li><img src="{{:~getPhotoURL(#view, 500)}}" /></li>{{/for}}
				</ul>
			{{else}}
				<img src="{{for photos}}{{:~getPhotoURL(#view, 500)}}{{/for}}" />
			{{/if}}
			{{:caption}}
			{{for #data tmpl="#tmpl-metadata"/}}
		</article>
	</script>
```

### Quote post

```html
	<script id="tmpl-quote" type="text/x-jsrender">
		<article id="post-{{:id}}" class="post-{{:type}}">
			<h1>{{:text}}</h1>
			{{:source}}
			{{for #data tmpl="#tmpl-metadata"/}}
		</article>
	</script>
```

### Text post

```html
	<script id="tmpl-text" type="text/x-jsrender">
		<article id="post-{{:id}}" class="post-{{:type}}">
			<h1>{{:title}}</h1>
			{{:body}}
			{{for #data tmpl="#tmpl-metadata"/}}
		</article>
	</script>
```

### Video post

```html
	<script id="tmpl-video" type="text/x-jsrender">
		<article id="post-{{:id}}" class="post-{{:type}}">
			{{:~getVideoEmbed(#view, 500)}}
			{{:caption}}
			{{for #data tmpl="#tmpl-metadata"/}}
		</article>
	</script>
```

### Metadata / Tag templates

```html
	<script id="tmpl-metadata" type="text/x-jsrender">
		{{if note_count > 0}}<p><small><a href="{{:post_url}}#notes">{{:note_count}} notes</a></small></p>{{/if}}
		{{if tags}}<ul class="tags">{{for tags tmpl="#tmpl-tag"/}}</ul>{{/if}}
	</script>

	<script id="tmpl-tag" type="text/x-jsrender">
		<li><a href="http://{{:~getHostname()}}/tagged/{{:#data}}">{{:#data}}</a></li>
	</script>
```