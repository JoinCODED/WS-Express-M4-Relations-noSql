We have'nt touched the `student` model, because we will apply another type of relationship to it.

A `student` can enroll in many `courses`, and a `course` can have many `student`s, hence the name, `many to many` relation.

1. To create this relation, in the `Course` model:

```js
const { model, Schema } = require('mongoose');

const CourseSchema = new Schema({
  name: String,
  teacherId: { type: Schema.Types.ObjectId, ref: 'Teacher' },
  students: [
    {
      type: Schema.Types.ObjectId,
      ref: 'Student',
    },
  ],
});

module.exports = model('Course', CourseSchema);
```

2. Now we will do the relation from the other side, in the `Student` model:

```js
const { model, Schema } = require('mongoose');

const StudentSchema = new Schema({
  name: String,
  courses: [
    {
      type: Schema.Types.ObjectId,
      ref: 'Course',
    },
  ],
});

module.exports = model('Student', StudentSchema);
```
