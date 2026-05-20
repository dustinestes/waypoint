<br><br>
<img align="right" src="../branding/icons/waypoint_standalonemark_lightbg.png" height="44" alt="waypoint">
<h1>Examples</h1>
<br clear="both">

Real-world patterns showing how to structure your repo and configure your `waypoint.yaml` for different learning styles and goals. Each example covers both elements together so you can see exactly how the folder layout and the YAML connect.

Use these as a starting point — copy, adapt, and make them your own.

<br>

---

## Single Subject — Deep Dive

**Scenario:** A learner preparing for a single certification or focused topic. All effort is organized within one subject, broken into logical phases from foundation to exam readiness. Local notes and lab files live alongside the YAML and are linked directly from each module.

### Folder Structure

```
waypoint/
├── notes/
│   └── cka/
│       └── foundations/
│           ├── what-is-kubernetes.md
│           └── cluster-architecture.md
├── labs/
│   └── cka/
│       └── pods/
│           └── README.md
├── waypoint.yaml
└── dashboard.html
```

### waypoint.yaml

```yaml
subjects:

  - id: cka
    title: "Certified Kubernetes Administrator"
    description: "Preparation for the CKA exam — from core concepts to hands-on cluster management"
    estimated_time: "60 hours"

    milestones:

      - id: foundations
        title: "Foundations"
        description: "Core Kubernetes concepts and cluster architecture"
        order: 1
        estimated_time: "10 hours"

        modules:

          - id: what-is-kubernetes
            title: "What is Kubernetes?"
            order: 1
            type: reading
            difficulty: beginner
            estimated_time: "1 hour"
            status: complete
            started_date: "2025-03-10"
            completed_date: "2025-03-10"
            resources:
              - type: external
                label: "Official Docs"
                url: "https://kubernetes.io/docs/concepts/overview/"
              - type: notes
                label: "My Notes"
                path: "notes/cka/foundations/what-is-kubernetes.md"

          - id: cluster-architecture
            title: "Cluster Architecture"
            order: 2
            type: reading
            difficulty: beginner
            estimated_time: "2 hours"
            status: in_progress
            started_date: "2025-03-11"
            completed_date:
            resources:
              - type: external
                label: "Official Docs"
                url: "https://kubernetes.io/docs/concepts/architecture/"
              - type: notes
                label: "My Notes"
                path: "notes/cka/foundations/cluster-architecture.md"

      - id: workloads
        title: "Workloads and Scheduling"
        description: "Pods, deployments, services, and resource management"
        order: 2
        estimated_time: "15 hours"

        modules:

          - id: pods
            title: "Pods"
            order: 1
            type: mixed
            difficulty: intermediate
            estimated_time: "2 hours"
            status: not_started
            started_date:
            completed_date:
            resources:
              - type: external
                label: "Docs"
                url: "https://kubernetes.io/docs/concepts/workloads/pods/"
              - type: lab
                label: "Pod Lab"
                path: "labs/cka/pods/README.md"

      - id: exam-prep
        title: "Exam Preparation"
        description: "Practice exams, timed labs, and final review"
        order: 3
        estimated_time: "10 hours"

        modules:

          - id: killer-sh-practice
            title: "Killer.sh Practice Exam"
            order: 1
            type: quiz
            difficulty: advanced
            estimated_time: "4 hours"
            status: not_started
            started_date:
            completed_date:
            resources:
              - type: external
                label: "Killer.sh"
                url: "https://killer.sh"
```

---

## Multiple Subjects — Complementary Learning

**Scenario:** A learner building toward a broader role that spans several technologies. Rather than the default `notes/<subject>/` layout, this example uses a **subject-first structure** — each subject gets its own root folder containing whatever content it needs. This works well when subjects are large and self-contained, and it demonstrates that `waypoint.yaml` paths can point anywhere in the repo.

### Folder Structure

```
waypoint/
├── python/
│   └── notes/
│       └── fundamentals/
│           └── syntax-and-types.md
├── sql/
│   └── notes/
│       └── querying/
│           └── select-statements.md
├── docker/
│   └── labs/
│       └── first-container/
│           └── README.md
├── waypoint.yaml
└── dashboard.html
```

### waypoint.yaml

```yaml
subjects:

  - id: python
    title: "Python"
    description: "Python programming — from first syntax to scripting and automation"
    estimated_time: "30 hours"

    milestones:

      - id: fundamentals
        title: "Fundamentals"
        order: 1
        estimated_time: "10 hours"

        modules:

          - id: syntax-and-types
            title: "Syntax and Data Types"
            order: 1
            type: reading
            difficulty: beginner
            estimated_time: "2 hours"
            status: complete
            started_date: "2025-02-01"
            completed_date: "2025-02-02"
            resources:
              - type: external
                label: "Python Docs"
                url: "https://docs.python.org/3/tutorial/"
              - type: notes
                label: "My Notes"
                path: "python/notes/fundamentals/syntax-and-types.md"

  - id: sql
    title: "SQL"
    description: "Relational database fundamentals and query writing"
    estimated_time: "20 hours"

    milestones:

      - id: querying
        title: "Querying Basics"
        order: 1
        estimated_time: "6 hours"

        modules:

          - id: select-statements
            title: "SELECT Statements"
            order: 1
            type: reading
            difficulty: beginner
            estimated_time: "1 hour"
            status: complete
            started_date: "2025-02-05"
            completed_date: "2025-02-05"
            resources:
              - type: external
                label: "SQLZoo"
                url: "https://sqlzoo.net/wiki/SELECT_basics"
              - type: notes
                label: "My Notes"
                path: "sql/notes/querying/select-statements.md"

  - id: docker
    title: "Docker"
    description: "Containerization fundamentals and local development workflows"
    estimated_time: "15 hours"

    milestones:

      - id: containers
        title: "Containers and Images"
        order: 1
        estimated_time: "5 hours"

        modules:

          - id: first-container
            title: "Running Your First Container"
            order: 1
            type: lab
            difficulty: beginner
            estimated_time: "1 hour"
            status: not_started
            started_date:
            completed_date:
            resources:
              - type: external
                label: "Docker Getting Started"
                url: "https://docs.docker.com/get-started/"
              - type: lab
                label: "First Container Lab"
                path: "docker/labs/first-container/README.md"
```

---

## Minimalist — Just Enough to Track

**Scenario:** A learner who wants progress tracking without the overhead of local files or detailed metadata. No content folders are needed at all — the repo is just the YAML and the dashboard. External links can still be added to modules, but nothing needs to live locally. The dashboard still renders progress bars, status badges, and the in-progress strip with only the required fields filled in.

### Folder Structure

```
waypoint/
├── waypoint.yaml
└── dashboard.html
```

### waypoint.yaml

```yaml
subjects:

  - id: networking
    title: "Networking Fundamentals"

    milestones:

      - id: tcp-ip
        title: "TCP/IP"

        modules:

          - id: osi-model
            title: "The OSI Model"
            status: complete

          - id: ip-addressing
            title: "IP Addressing and Subnetting"
            status: in_progress

          - id: routing
            title: "Routing Basics"
            status: not_started

      - id: dns
        title: "DNS"

        modules:

          - id: how-dns-works
            title: "How DNS Works"
            status: not_started

          - id: record-types
            title: "DNS Record Types"
            status: not_started
```

---

## Certification Sprint — Focused and Time-Boxed

**Scenario:** A learner with an exam date on the calendar, working backward from a deadline. Lower-priority modules are pre-marked `skipped` to keep the path lean and focused. `estimated_time` is used at every level so the total remaining commitment is always visible.

### Folder Structure

```
waypoint/
├── notes/
│   └── aws-saa/
│       └── core-services/
│           └── s3-deep-dive.md
├── waypoint.yaml
└── dashboard.html
```

### waypoint.yaml

```yaml
subjects:

  - id: aws-saa
    title: "AWS Solutions Architect Associate"
    description: "SAA-C03 exam preparation — 6 week sprint"
    estimated_time: "80 hours"

    milestones:

      - id: core-services
        title: "Core Services"
        description: "EC2, S3, RDS, VPC — the foundation of every exam question"
        order: 1
        estimated_time: "20 hours"

        modules:

          - id: ec2-fundamentals
            title: "EC2 Fundamentals"
            order: 1
            type: video
            difficulty: beginner
            estimated_time: "3 hours"
            status: complete
            started_date: "2025-04-01"
            completed_date: "2025-04-02"
            resources:
              - type: external
                label: "AWS Skill Builder"
                url: "https://skillbuilder.aws"

          - id: s3-deep-dive
            title: "S3 Storage Classes and Lifecycle"
            order: 2
            type: mixed
            difficulty: intermediate
            estimated_time: "4 hours"
            status: in_progress
            started_date: "2025-04-03"
            completed_date:
            resources:
              - type: external
                label: "S3 Docs"
                url: "https://docs.aws.amazon.com/s3/"
              - type: notes
                label: "My Notes"
                path: "notes/aws-saa/core-services/s3-deep-dive.md"

      - id: advanced-topics
        title: "Advanced Topics"
        description: "Lower-weighted domains — skipped to protect study time"
        order: 2
        estimated_time: "10 hours"

        modules:

          - id: cognito
            title: "Amazon Cognito"
            order: 1
            type: reading
            difficulty: intermediate
            estimated_time: "1 hour"
            status: skipped

          - id: appflow
            title: "Amazon AppFlow"
            order: 2
            type: reading
            difficulty: intermediate
            estimated_time: "30 minutes"
            status: skipped

      - id: practice-exams
        title: "Practice Exams"
        description: "Timed full-length practice under exam conditions"
        order: 3
        estimated_time: "12 hours"

        modules:

          - id: practice-exam-1
            title: "Practice Exam 1"
            order: 1
            type: quiz
            difficulty: advanced
            estimated_time: "3 hours"
            status: not_started
            started_date:
            completed_date:
            resources:
              - type: external
                label: "Tutorials Dojo"
                url: "https://tutorialsdojo.com"
```

---

## Lifelong Learner — Professional Portfolio

**Scenario:** A developer who points employers to GitHub as a portfolio and wants a single, beautiful place to showcase their entire learning history — across years, across platforms. Instead of sending a hiring manager to five separate platform profiles, this waypoint is hosted on GitHub Pages and tells the full story in one view.

Each completed course links to both the learner's profile on the originating platform (for independent validation) and a local certificate file stored in the repo. Employers can expand a subject, see time invested, start and completion dates, verify via the platform profile, and download the certificate — all without leaving the page.

The folder structure is intentionally minimal. Almost everything is external. The only local content is a `certifications/` folder holding completion certificates as they are earned.

> **Note:** Certificate files are linked using `type: notes` as a practical workaround — a dedicated `docs` resource type is planned for a future release. See [GitHub issue #6](https://github.com/dustinestes/waypoint/issues/6).

### Folder Structure

```
waypoint/
├── certifications/
│   ├── backend-development/
│   │   └── bootdev-backend-path-certificate.pdf
│   └── cloud/
│       ├── aws-saa-certificate.pdf
│       └── azure-az900-certificate.pdf
├── waypoint.yaml
└── dashboard.html
```

### waypoint.yaml

```yaml
subjects:

  - id: backend-development
    title: "Backend Development"
    description: "Full backend learning path — languages, databases, and systems design"
    estimated_time: "320 hours"

    milestones:

      - id: bootdev-backend-path
        title: "Boot.dev Backend Learning Path"
        description: "Structured backend curriculum covering Python, Go, algorithms, and systems"
        order: 1
        estimated_time: "200 hours"

        modules:

          - id: bootdev-python
            title: "Learn Python"
            order: 1
            type: video
            difficulty: beginner
            estimated_time: "30 hours"
            status: complete
            started_date: "2023-01-10"
            completed_date: "2023-03-04"
            resources:
              - type: external
                label: "Boot.dev Profile"
                url: "https://www.boot.dev/u/your-username"

          - id: bootdev-algorithms
            title: "Learn Algorithms and Data Structures"
            order: 2
            type: mixed
            difficulty: intermediate
            estimated_time: "40 hours"
            status: complete
            started_date: "2023-03-05"
            completed_date: "2023-06-18"
            resources:
              - type: external
                label: "Boot.dev Profile"
                url: "https://www.boot.dev/u/your-username"

          - id: bootdev-go
            title: "Learn Go"
            order: 3
            type: video
            difficulty: intermediate
            estimated_time: "35 hours"
            status: complete
            started_date: "2023-07-01"
            completed_date: "2023-10-22"
            resources:
              - type: external
                label: "Boot.dev Profile"
                url: "https://www.boot.dev/u/your-username"
              - type: notes
                label: "Certificate"
                path: "certifications/backend-development/bootdev-backend-path-certificate.pdf"

  - id: cloud-platforms
    title: "Cloud Platforms"
    description: "Public cloud certifications — AWS and Azure"
    estimated_time: "120 hours"

    milestones:

      - id: aws
        title: "Amazon Web Services"
        order: 1
        estimated_time: "60 hours"

        modules:

          - id: aws-saa
            title: "AWS Solutions Architect Associate (SAA-C03)"
            order: 1
            type: mixed
            difficulty: intermediate
            estimated_time: "60 hours"
            status: complete
            started_date: "2023-11-01"
            completed_date: "2024-02-14"
            resources:
              - type: external
                label: "Credly Badge"
                url: "https://www.credly.com/users/your-username"
              - type: notes
                label: "Certificate"
                path: "certifications/cloud/aws-saa-certificate.pdf"

      - id: azure
        title: "Microsoft Azure"
        order: 2
        estimated_time: "60 hours"

        modules:

          - id: az-900
            title: "Microsoft Azure Fundamentals (AZ-900)"
            order: 1
            type: mixed
            difficulty: beginner
            estimated_time: "20 hours"
            status: complete
            started_date: "2024-03-01"
            completed_date: "2024-04-15"
            resources:
              - type: external
                label: "Microsoft Learn Profile"
                url: "https://learn.microsoft.com/en-us/users/your-username"
              - type: notes
                label: "Certificate"
                path: "certifications/cloud/azure-az900-certificate.pdf"

          - id: az-104
            title: "Microsoft Azure Administrator (AZ-104)"
            order: 2
            type: mixed
            difficulty: intermediate
            estimated_time: "40 hours"
            status: in_progress
            started_date: "2025-01-06"
            completed_date:
            resources:
              - type: external
                label: "Microsoft Learn Profile"
                url: "https://learn.microsoft.com/en-us/users/your-username"
```

<br>

---

<img align="left" src="../branding/banners/waypoint_banner_lightbg.png" height="64" alt="waypoint">
<div align="right">v1.0.0</div>
<br clear="both">
