1. To enroll a `student` in a `course`, we need to create a new route in `courses` routes:

```js
router.post('/:courseId/:studentId', courseEnroll);
```

We need the `course` id and the `student` id as params.

2. Let's create the `courseEnroll` function in our `courses` controller:

```js
exports.courseEnroll = async (req, res, next) => {
  try {
    const { studentId } = req.params;
    res.status(204).end();
  } catch (error) {
    next(error);
  }
};
```

3. OK, so we have the data we need, now we need to insert this `student` into the `course`. And the `course` in this `student`.

```js
exports.courseEnroll = async (req, res, next) => {
  try {
    const { studentId } = req.params;
    await Course.findByIdAndUpdate(req.course.id, {
      $push: { students: studentId },
    });
    await Student.findByIdAndUpdate(studentId, {
      $push: { courses: req.course.id },
    });

    res.status(204).end();
  } catch (error) {
    next(error);
  }
};
```

4. Check your database, it works!
