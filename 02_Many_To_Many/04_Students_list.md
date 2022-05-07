We will do the same in our `students` controller:

```js
exports.studentsGet = async (req, res, next) => {
  try {
    const students = await Student.find({}, '-createdAt -updatedAt').populate(
      'courses',
      'name'
    );
    res.json(students);
  } catch (error) {
    next(error);
  }
};
```
