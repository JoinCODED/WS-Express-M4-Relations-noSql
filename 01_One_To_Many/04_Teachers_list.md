1. Let's fetch the list of `teachers` in Postman. Okay, nothing special about it. But what if we can add to every `teacher` the list of its `courses`!

2. Right now what we will get is the `id`s of the `courses`, we need to replace them with the whole object using the `populate` method and pass it the field we want to populate:

```js
exports.teachersGet = async (req, res, next) => {
  try {
    const teachers = await Teacher.find({}, '-createdAt -updatedAt').populate(
      'courses'
    );
    res.json(teachers);
  } catch (error) {
    next(error);
  }
};
```
