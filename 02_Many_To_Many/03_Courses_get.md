We want our `courses` list to include all `students` enrolled.

1. In `courses` controller, chain the `populate` method with another `populate` method:

```js
exports.coursesGet = async (req, res, next) => {
  try {
    const courses = await Course.find({}, '-createdAt -updatedAt')
      .populate('teacherId', 'name')
      .populate('students', 'name');
    res.json(courses);
  } catch (error) {
    next(error);
  }
};
```
