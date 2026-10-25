# Hostel Complaint Management — API

Backend for a hostel complaint system. **Students** raise complaints in a category, **admins**
assign them to **workers**, and everyone can follow the status from *Pending* to *Resolved*.

![Node.js](https://img.shields.io/badge/Node.js-0F2540?style=flat-square&logo=nodedotjs&logoColor=5FA04E)
![Express](https://img.shields.io/badge/Express-0F2540?style=flat-square&logo=express&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-0F2540?style=flat-square&logo=mongodb&logoColor=47A248)

> Status: the REST API is done; a web frontend is planned. Full requirements are in
> [`docs/Hostel_Complaint_Management_Requirements.md`](docs/Hostel_Complaint_Management_Requirements.md).

## Features

- **Roles** — `student`, `admin`, `worker`, enforced per route (`authenticate` + `authorize`)
- **Complaints** — categories: electricity, cleanliness, food, plumber, carpenter, other
- **Workflow** — Pending → Assigned → In Progress → Resolved, with comments on each complaint
- **Role-scoped lists** — students see their own complaints, workers see the ones assigned to them, admins see all
- **Security basics** — bcrypt passwords, JWT, Joi validation, helmet, central error handler

## API

| Method | Route | Who | What it does |
| --- | --- | --- | --- |
| POST | `/api/auth/register` | anyone | Create an account |
| POST | `/api/auth/login` | anyone | Log in, returns a JWT |
| POST | `/api/complaints` | student | Raise a complaint |
| GET | `/api/complaints` | all roles | List complaints (scoped by role) |
| GET | `/api/complaints/:id` | owner / staff | One complaint with comments |
| PUT | `/api/complaints/:id/assign` | admin | Assign a worker |
| PUT | `/api/complaints/:id/status` | worker / admin | Update the status |
| POST | `/api/complaints/:id/comments` | all roles | Add a comment |

## Run it locally

```bash
cp .env.example .env      # set MONGO_URI and JWT_SECRET
npm install
npm run dev               # http://localhost:4000
node backend/script/seed.js   # optional sample data
```
