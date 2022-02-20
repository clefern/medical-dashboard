# Problem Description

You were hired to develop a system for doctors of a hospital to keep track of their daily appointments. In this system a doctor will be able to see:

- Their week calendar
- The history of their last appointments
- Their list of patients
- Detailed information about each patient and their appointments

For this challenge we’re gonna consider that this doctor only works from monday to friday, from 9AM to 6PM and the appointments can last 30min or an hour and can only start every 30min of the doctor’s working shift.

The mocks are at the end of this document.

## Requirements

The application consists of two pages:

### Doctor’s dashboard index

This is the starting point for the user and is divided into three sections:

1. Weekly calendar: We should show all the appointments of the current week, from monday to friday, including the past and future ones. Every appointment should have some visual indication of who’s the patient, and the appointment description, type and status. This should preferably be displayed in a calendar-like view. The application should only show the current week, you don’t need to worry about the next weeks after that.
2. Appointments history: The second section is a list of all the past appointments of the doctor, displaying the patient name, and the appointment time, status and type.
3. Patients list: A list of all the doctor’s patients. This list should be divided into pages of 10 items.

For all these sections if the user clicks one of the items they’ll be taken to the Patient details page, but for the items of the sections 1 and 2 the Patient page needs to render with that particular appointment initially shown from start.

### Patient details

This page is accessed after interacting with one of the items from the Doctor’s dashboard index and is also divided into sections:

1. Patient info: This section contains the general information about the patient, like name, document (formatted as XXX.XXX.XXX-XX), health system ID (formatted as XXX.XXX/XXXX), birthday and age.
2. Appointments: A list with all the past, current and future appointments should be shown for the given patient. When one of the items from this section is clicked the data for that item should be loaded from the API and details about the appointment should be shown, these details include the description, notes (that should be editable by the doctor if the appointment is pending), start time, end time (if any), status, specialty and type. The doctor should be able to see the details for more than one appointment at the same time. This list should be divided into pages of 10 items.
3. Patient plan: The insurance plan of the patient
4. Date of the last appointment
5. A list of recent, upcoming and history of appointments: it should be separated into tabs or other convenient visual separation

## The API

The API that will be consumed by the application contains the following endpoints. The description of each custom type is at the end of this section. It’s important to mention that the API can fail for some reason and it should affect the user experience the less the possible. The URL for the API is https://cm42-medical-dashboard.herokuapp.com/ and **only** the endpoints listed here should be used.

### GET /patients

This endpoint returns an array of patients with this schema:

```ts
{
  id: number,
  name: string,
  document: string,
  healthSystemId: string,
  birthday: string,
  insurancePlan: InsurancePlan
}
```

### GET /patients/:id

This endpoint returns a patient with this schema:

```ts
{
  id: number,
  name: string,
  document: string,
  healthSystemId: string,
  birthday: string,
  insurancePlan: InsurancePlan
}
```

### GET /appointments

This endpoint returns an array of appointments with this schema:

```ts
{
  id: number,
  specialty: Specialty,
  type: AppointmentType,
  description: string,
  notes: string,
  patientId: number,
  startTime: string,
  endTime: string | null
  status: Status
}
```

### GET /appointments/:id

This endpoint returns an appointments with this schema:

```ts
{
  id: number,
  specialty: Specialty,
  type: AppointmentType,
  description: string,
  notes: string,
  patientId: number,
  startTime: string,
  endTime: string | null
  status: Status
}
```

### API Types

AppointmentType:
- firstVisit
- followUp
- checkUp
- exam
- surgery

Specialty:
- neurology
- cardiology
- general

Status:
- pending
- completed
- cancelled
- absent

InsurancePlan:
- Regional
- National Basic
- National Premium
- International
- Diamond

## Technical requirements

- No authentication is necessary
- You should document the setup and execution of both the application and the tests
- The implementation **should** be mobile-friendly. It’s allowed to simplify or adapt features when it’s displayed on a mobile screen.
- All the possible errors **should** be handled, making the user experience the more pleasant the possible.
- The mocks are mostly a general idea of what should be included in your implementation but you don't need to mimic it if desired, including the positioning, icons and the such
- Unit tests are **required**.
- End-to-end tests are desired.
- All the CSS used in the application should be written by the candidate. The use of CSS-in-JS is allowed.
- If you publish this code to your GitLab or GitHub account, make sure it's **PRIVATE**
- If you prefer to share a zip file in Google Drive or Dropbox, make sure you **REMOVE** the node_modules directory

## Extras

If you have finished all the previous features and want extra desired features to work on:

- Sections reorganization: Allow the user to reorganize the order of or hide/show sections of each page and persist it in the browser storage in a way that if the user refreshes the page the order is kept. If a section is hidden and then reshown, it should be shown as the last of the sections.
- Animation during page transitions: Add an animation when the user goes from the index page to the details page.

## Mocks

### Home page (desktop, tablet and mobile, in this order)

![home desktop](https://user-images.githubusercontent.com/4325587/116892997-d5b32200-ac06-11eb-8539-f81b6555d299.png)
![home tablet](https://user-images.githubusercontent.com/4325587/116892985-d2b83180-ac06-11eb-8752-552a30765f5c.png)
![home mobile](https://user-images.githubusercontent.com/4325587/116892993-d51a8b80-ac06-11eb-8afe-32985dbbd9b6.png)

### Patient page (desktop, tablet and mobile, in this order)

![patient desktop](https://user-images.githubusercontent.com/4325587/116893001-d77ce580-ac06-11eb-9c66-d640bea5576c.png)
![patient tablet](https://user-images.githubusercontent.com/4325587/116892990-d481f500-ac06-11eb-80b0-c0104b8a8c12.png)
![patient mobile](https://user-images.githubusercontent.com/4325587/116892992-d51a8b80-ac06-11eb-83dc-9de5399004fe.png)