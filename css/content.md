### content property

CSS has a property called content. It can only be used with the pseudo
elements :after and :before. It is written like a pseudo selector (with the
colon), but it's called a pseudo element because it's not actually selecting
anything that exists on the page but adding something new to the page. This is
what it looks like:

  <ul>
  <li class="email">example@gmail.com</li>
  </ul>

  .email:before { content: "Email address: "; }

  output: Email address: example@gmail.com

