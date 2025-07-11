
# Recursion: Nested Comments System using Recursion

## Use Case:
You're building a comments section where each comment can have replies, and those replies can have more replies — forming a tree-like structure.

---

## Example Data:
```js
const comments = [
  {
    id: 1,
    text: "This is the first comment",
    replies: [
      {
        id: 2,
        text: "First reply",
        replies: [
          {
            id: 3,
            text: "Nested reply",
            replies: []
          }
        ]
      }
    ]
  },
  {
    id: 4,
    text: "Second top-level comment",
    replies: []
  }
];
```

---

## Recursive Function to Display Comments

```js
function displayComments(comments, indent = 0) {
  for (let comment of comments) {
    console.log(' '.repeat(indent) + comment.text);

    // Recursively display replies with increased indent
    if (comment.replies && comment.replies.length > 0) {
      displayComments(comment.replies, indent + 2);
    }
  }
}

displayComments(comments);
```

---

## Output:
```
This is the first comment
  First reply
    Nested reply
Second top-level comment
```

---

## Explanation:
- Each comment is printed with a left indent (`' '.repeat(indent)`) to simulate nesting.
- If a comment has replies, we recursively call `displayComments` on those replies with more indent.
- The recursion keeps going until there are no more replies.

---

## Where It's Useful:
- Nested UI components (like replies in a blog or app like Reddit)
- JSON tree rendering
- Collapsible menus or sidebars


