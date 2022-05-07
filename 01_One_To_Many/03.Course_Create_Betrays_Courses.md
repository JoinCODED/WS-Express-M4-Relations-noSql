Hmmmmm, so now whenever we create a new `course` we need to add the `Teacher` ID. The easiest way to do that is to pass the `teacher` ID in the request body. But that's not the correct convention, we agreed before that IDs are passed in the request's URL.

1. So we will change our `createCourse` route to `/teachers/:teacherId/courses`. Since it starts with `teachers`, we will move the `createCourse` route and controller to the `teacher`'s routes and controllers files.

2. Now we have to do 3 steps,1: Add the `teacherId` to `req.body` 2: Create the `course`, 3: adding this created `course` in the `courses` array in the `teacher` model.

Step 1:

```js
try {
    [...]
    req.body.teacherId = req.teacher.id;
    [...]
  }
```

Step 2:

```js
try {
    [...]
    const newCourse = await Course.create(req.body);
    [...]
  }
```

Step 3:

```js
exports.coursesCreate = async (req, res, next) => {
  try {
    const newCourse = await Course.create(req.body);
    await Teacher.findByIdAndUpdate(req.teacher.id, {
      $push: { courses: newCourse._id },
    });
    res.status(201).json(newCourse);
  } catch (error) {
    next(error);
  }
};
```

3. Let's try creating another course.

4. That Worked!.
