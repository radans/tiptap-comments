# TipTap comments extension

Extension is written in typescript

Comments are saved in extensions storage. When comment is added, thread is created and all comments
regarding that thread are inserted there.
Structure

```json
[
  {
    "threadId": "uuid",
    "comments": [
      {
        "comment": "text",
        "uuid": "uuid",
        "date": "date-time",
        "user": {},
        "parent_id": "nullable",
        "parent_text": "nullable"
      }
    ]
  }
]
```

### Usage

```js
import customComment from "@rcode-link/tiptap-comments";

const editor = Editor({
    extensions: [
        StarterKit,
        customComment
    ]
})
```

### Define User who is posting:

The user object can be whatever is passed to it

```js
import customComment from "@rcode-link/tiptap-comments";

const editor = Editor({
    extensions: [
        StarterKit,
        customComment.configure({
            user: {
                firstName: user.firstName,
                lastName: user.lastName,
                id: user.id
            }
        })
    ]
})


```

### Add comment and Reply

Comment:

```js
editor.commands.addComments({
    comment: commentTest
})
```

Reply:

```js
editor.commands.addComments({
    comment: commentTest,
    parent_id: id_OF_parent
})
```

### Remove comment

```js
editor.commands.removeSpecificComment(threadId, commentUuid);
```

### Getting list of comments

```js
editor.storage.comment.comments
```

**Note:**
Since comments are saved in extension storage, it is necessary when saving data to grab them, and on load to add them
back

Adding comments when loaded:

```js
editor.commands.setContent(content, true);
editor.storage.comment.comments = comments;
```
Getting comments to be saved: 
```js
editor.storage.comment
```
TODO:

* update comment
