---
layout: default
title: Contacts
---

<div id="contact">
  <h1 class="pageTitle">Contact Me</h1>
  <div class="contactContent">
    <p class="intro">Если я по какой-то причине вам понадоблюсь, то вот мои координаты:</p>
    <p></p>
    <ul>
		<li>ВКонтакте: <a href="https://vk.com/{{ site.social.vkontakte }}">https://vk.com/goha20777</a></li>
  		<li>Skype: goha20777</li>
  		<li>Facebook: <a href="https://www.facebook.com/{{ site.social.facebook }}">https://www.facebook.com/goha20777</a></li>
		<li>E-mail: <a href="mailto:{{ site.social.email }}">gosha20777@live.ru</a></li>
  	</ul>
  </div>
  <form method="POST" action="http://formspree.io/gosha20777@live.ru">
  	<input name="email" placeholder="Your email" type="email">
  	<textarea name="message" placeholder="Your message"></textarea>
  	<button type="submit" class="button">Send</button>
  </form>
  <!--
  <form action="https://formspree.io/gosha20777@live.ru" method="POST">
    <label for="name">Name</label>    
    <input type="text" id="name" name="name" class="full-width"><br>
    <label for="email">Email Address</label>
    <input type="email" id="email" name="_replyto" class="full-width"><br>
    <label for="message">Message</label>
    <textarea name="message" id="message" cols="30" rows="10" class="full-width"></textarea><br>
    <input type="submit" value="Send" class="button">
  </form> -->
</div>
