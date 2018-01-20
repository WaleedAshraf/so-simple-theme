---
layout: page
title: Contact me!
excerpt: "Don't feel free to ask anything :D"
modified: 2014-08-08T19:44:38.564948-04:00
footer: not
image:
  feature: cover_build.jpg
  credit: kanhangadvartha
  creditlink: http://www.kanhangadvartha.com/HQW-61617.html
---

<div class="contact-page">
  <ul>
    {% if site.owner.email %}<li><a href="mailto:{{site.owner.email}}" title="{{site.owner.name}} Email" target="_blank"><i class="fa fa-envelope-square fa-2x"></i>Email: {{site.owner.email}}</a></li>{% endif %}
    {% if site.owner.github %}<li><a href="https://github.com/{{site.owner.github}}" title="{{site.owner.name}} on Github" target="_blank"><i class="fa fa-github-square fa-2x"></i>Github: {{site.owner.github}}</a></li>{% endif %}
    {% if site.owner.medium %}<li><a href="https://medium.com/@{{site.owner.medium}}" title="{{site.owner.medium}} on Medium" target="_blank"><i class="fa fa-medium fa-2x"></i>Medium: {{site.owner.medium}}</a></li>{% endif %}
    {% if site.owner.flickr %}<li><a href="https://www.flickr.com/photos/{{site.owner.flickr}}" title="{{site.owner.name}} on Flickr" target="_blank"><i class="fa fa-flickr fa-2x"></i>Flickr: {{site.owner.flickr}}</a></li>{% endif %}
    {% if site.owner.tumblr %}<li><a href="http://{{site.owner.tumblr}}.tumblr.com" title="{{site.owner.name}} on Tumblr" target="_blank"><i class="fa fa-tumblr-square fa-2x"></i>Tumblr: {{site.owner.tumblr}}</a></li>{% endif %}
    {% if site.owner.linkedin %}<li><a href="https://linkedin.com/in/{{site.owner.linkedin}}" title="{{site.owner.name}} on LinkedIn" target="_blank"><i class="fa fa-linkedin-square fa-2x"></i>LinkedIn: {{site.owner.linkedin}}</a></li>{% endif %}
    {% if site.owner.twitter %}<li><a href="https://twitter.com/{{site.owner.twitter}}" title="{{site.owner.name}} on Twitter" target="_blank"><i class="fa fa-twitter-square fa-2x"></i>Twitter: {{site.owner.twitter}}</a></li>{% endif %}
    {% if site.owner.facebook %}<li><a href="https://facebook.com/{{site.owner.facebook}}" title="{{site.owner.name}} on Facebook" target="_blank"><i class="fa fa-facebook-square fa-2x"></i>Facebook: {{site.owner.facebook}}</a></li>{% endif %}
    {% if site.owner.google.plus %}<li><a href="https://plus.google.com/+{{site.owner.google.plus}}" title="{{site.owner.name}} on Google+" target="_blank"><i class="fa fa-google-plus-square fa-2x"></i>Google+: {{site.owner.google.plus}}</a></li>{% endif %}
    {% if site.owner.instagram %}<li><a href="https://instagram.com/{{site.owner.instagram}}" title="{{site.owner.name}} on Instagram" target="_blank"><i class="fa fa-instagram fa-2x"></i>Instagram: {{site.owner.instagram}}</a></li>{% endif %}
    {% if site.owner.pinterest %}<li><a href="https://www.pinterest.com/{{site.owner.pinterest}}/" title="{{site.owner.name}} on Pinterest" target="_blank"><i class="fa fa-pinterest fa-2x"></i>Pinterest: {{site.owner.pinterest}}</a></li>{% endif %}
    {% if site.owner.weibo %}<li><a href="https://www.weibo.com/u/{{site.owner.weibo}}/" title="{{site.owner.name}} on Weibo" target="_blank"><i class="fa fa-weibo fa-2x"></i>webio: {{site.owner.name}}</a></li>{% endif %}
    {% if site.owner.stackexchange %}<li><a href="{{site.owner.stackexchange}}" title="{{site.owner.name}} on StackExchange" target="_blank"><i class="fa fa-stack-exchange fa-2x"></i>StackExchange: waleed-ashraf</a></li>{% endif %}
    {% if site.owner.behance %}<li><a href="https://www.behance.net/{{site.owner.behance}}" title="{{site.owner.name}} on Behance" target="_blank"><i class="fa fa-behance-square fa-2x"></i>Behance: {{site.owner.behance}}</a></li>{% endif %}
  </ul>
</div><!-- /.social-icons -->