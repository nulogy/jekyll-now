---
layout: post
title: "async/await Keywords of ES7 for Simpler Promises"
author: shahriyarnasir
date: 2017-03-28T22:04:23+00:00
---

ES7 introduces the `async`/`await` keywords. They are mostly syntactic sugar on top of Promises. You can write cleaner more readable asynchronous tasks code.

NOTE: They are available in Node 7.6.0 also.

## Example:

Here is some code for programmatically creating a coding exercise for a developer candidate that has applied to us. We've improved the readability of it using `async`/`await`.

This hard to read test which uses Promises:

```javascript
it('returns any errors that may have occurred', () => {
  return automator
    .getRepo()
    .then(repo => !repo ? automator.createExercise() : Promise.resolve())
    .then(() => this.room.user.say('alice', `hubot create coding exercise repo for ${candidateEmail}`))
    .then(() => {
      expect(lastBotMessage()).to.contain(`Error creating coding exercise for *${candidateEmail}*:`)
    });
});
```

Becomes this:

```javascript
it('returns any errors that may have occurred', async() => {
  let repo = await automator.getRepo();
  if (!repo) {
    await automator.createExercise();
  }

  await this.room.user.say('alice', `hubot create coding exercise repo for ${candidateEmail}`);

  expect(lastBotMessage()).to.contain(`Error creating coding exercise for *${candidateEmail}*:`)
});
```

Which reads more like an Arrange/Act/Assert style test.
