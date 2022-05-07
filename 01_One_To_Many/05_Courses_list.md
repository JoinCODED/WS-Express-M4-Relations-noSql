We'll fix our `courses` list to return all `courses`, but to also add the `teacher`'s name to display it in the `courses` list.

1. Now let's populate the `teacherId` field in the `course` item. In `courses` Controller:

```js
exports.coursesGet = async (req, res, next) => {
  try {
    const courses = await Course.find({}, '-createdAt -updatedAt').populate(
      'teacherId',
      'name'
    );
    res.json(courses);
  } catch (error) {
    next(error);
  }
};
```

2. By passing `populate` a second argument, we are selecting which fields to get from the `teacher` model.
