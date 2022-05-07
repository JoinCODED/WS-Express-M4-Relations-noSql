1. Now let's create the relationship between our two models, `Teacher` and `Course`. Let's think about it, every `Teacher` can have many `courses`, but every `course` can have one `teacher` only. So, it's a one-to-many relationship.

2. We will define our relationships in the `course` model, we will add a new field called `courses` and this field will be an array since it has many items:

```js
const { model, Schema } = require('mongoose');

const TeacherSchema = new Schema({
  name: String,
  courses: [],
});

module.exports = model('Teacher', TeacherSchema);
```

3. Next, we will tell mongoose that the type of those items is an `ObjectId`, which is the type of any mongoose document:

```js
const { model, Schema } = require('mongoose');

const TeacherSchema = new Schema({
  name: String,
  courses: [
    {
      type: Schema.Types.ObjectId,
    },
  ],
});

module.exports = model('Teacher', TeacherSchema);
```

4. We also need to tell mongoose the reference of this `ObjectId`, which model are we referring:

```js
const { model, Schema } = require('mongoose');

const TeacherSchema = new Schema({
  name: String,
  courses: [
    {
      type: Schema.Types.ObjectId,
      ref: 'Course',
    },
  ],
});

module.exports = model('Teacher', TeacherSchema);
```

5. We will do the same thing from the other side, the `course` model, and this time its only one `teacher`, not an array:

```js
const { model, Schema } = require('mongoose');

const CourseSchema = new Schema({
  name: String,
  teacherId: { type: Schema.Types.ObjectId, ref: 'Teacher' },
});

module.exports = model('Course', CourseSchema);
```
