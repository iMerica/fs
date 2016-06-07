# FS

FS is a radical new concept that proposes: everything teams need for issue tracking and project 
management can be done using only a unix file system. In the following steps I'll show you
how to track a new software project using FS.

### Epics
Large high level business goals that represent multiple user stories are known as "Epics". Lets 
create two example epics for a mobile app that uses Facebook for authentication and
allows users to bookmark posts.

```bash
$ mkdir -p epics/{facebook_login,bookmarks}

```

### User Stories

Within each Epic we have user stories. User stories represent some particular value for the customer.
To start with, lets give each epic 5 user stories. Lets also keep user stories in one of three states:
backlog, in progress, done.

```bash
$ find epics -maxdepth 1 -mindepth 1 -exec mkdir -p {}/user_stories/{backlog,in_progress,done} \;

```

and create the actual story files that we can fill out later.

```bash
$ find epics -type d -name 'backlog' -exec touch {}/story_{1..5}.md \;

```

Now lets create a README.md file for every directory so we can describe what each directory represents.

```bash
$ find epics -type d -exec touch {}/README.md \;

```

### Agile Workflow

To assign user stories to yourself, simply change the owner of the file.

```bash
$ chown $USER epics/facebook_login/user_stories/backlog/story_1.md

```

Then update its status to in progress

```
$ mv epics/facebook_login/user_stories/backlog/story_1.md epics/facebook_login/user_stories/in_progress/story_1.md

```

Once your done, you can move its status to the done directory

```bash
$ mv epics/facebook_login/user_stories/in_progress/story_1.md epics/facebook_login/user_stories/done/story_1.md

```

To view all stories currently assigned to yourself,

```bash
$ find epics -type f -name 'story*.md' -user $USER 

```

To view the entire hierarchy

```bash
$ tree
.
├── README.md
└── epics
    ├── README.md
    ├── facebook_login
    │   ├── README.md
    │   └── user_stories
    │       ├── README.md
    │       ├── backlog
    │       │   ├── README.md
    │       │   ├── story_1.md
    │       │   ├── story_2.md
    │       │   ├── story_3.md
    │       │   ├── story_4.md
    │       │   └── story_5.md
    │       ├── done
    │       │   └── README.md
    │       └── in_progress
    │           └── README.md
    └── bookmarks
        ├── README.md
        └── user_stories
            ├── README.md
            ├── backlog
            │   ├── README.md
            │   ├── story_2.md
            │   ├── story_3.md
            │   ├── story_4.md
            │   └── story_5.md
            ├── done
            │   └── README.md
            └── in_progress
                ├── README.md
                └── story_1.md

11 directories, 22 files

```




