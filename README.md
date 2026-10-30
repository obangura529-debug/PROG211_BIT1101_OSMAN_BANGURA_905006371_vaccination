# OOP1 Assignment - Vaccination Tracker

## Module
PROG211 - Object-Oriented Programming 1

## Project
Real-World Solutions under Digital Public Goods (DPG) Standards

## Domain
Health - Vaccination Tracker

## 1. Project Overview

This project is a simple Python vaccination tracking program developed using
Object-Oriented Programming (OOP). It demonstrates classes, objects, attributes,
methods and one Python data structure.

The system allows a vaccination center to register patient objects and record
basic vaccination information.

The program deliberately uses a simple non-sensitive patient identifier rather
than storing sensitive medical information.

## 2. OOP Concepts Used

### Class 1: Patient
Attributes:
- patient_id
- name
- age
- vaccinations

Methods:
- add_vaccination()
- display_info()
- get_total_patients() - class method
- is_valid_age() - static method

### Class 2: VaccinationCenter
Attributes:
- center_name
- location
- patients

Methods:
- register_patient()
- display_patients()
- from_default_location() - class method
- count_vaccinated() - static method

## 3. Python Data Structure

The program uses ONE main data structure as required: a list.

The list named `patients` stores several Patient objects:

```python
patients = []
```

Patients are added using:

```python
add_patient(patients, patient1)
```

The records can then be displayed by looping through the list.

## 4. Methods

### Instance methods
Examples:
- `patient.add_vaccination(...)`
- `patient.display_info()`
- `center.register_patient(...)`

Instance methods work with a particular object.

### Class methods
Examples:
- `Patient.get_total_patients()`
- `VaccinationCenter.from_default_location(...)`

Class methods use the `@classmethod` decorator and operate at class level.

### Static methods
Examples:
- `Patient.is_valid_age(...)`
- `VaccinationCenter.count_vaccinated(...)`

Static methods perform useful operations that do not require a specific
object instance.

## 5. DPG Standards Alignment

### Open-source
The source code is written in Python and can be uploaded to a public GitHub
repository so that others can inspect, reuse and improve it.

### Inclusive and accessible design
The program uses simple text output and straightforward functions. It does not
depend on expensive or specialized software.

### Privacy-respecting
The system is designed as a demonstration and avoids storing sensitive medical
information. It uses basic identifiers and vaccination entries only.

### Modular and reusable
The program is divided into classes and functions. The Patient and
VaccinationCenter classes can be reused or expanded for other vaccination
programs.

## 6. Sample Output

```
Total Patient Objects: 3

Vaccination Center: Central Vaccination Center
Location: Freetown, Sierra Leone
----------------------------------------
Patient ID: P001
Name: Mariama
Age: 25
Vaccinations:
  - COVID-19 (Dose 1)
  - COVID-19 (Dose 2)

Patient ID: P002
Name: Mohamed
Age: 8
Vaccinations:
  - Measles (Dose 1)
  - Polio (Dose 1)

Patient ID: P003
Name: Fatmata
Age: 31
Vaccinations:
  - Tetanus (Dose 1)

Patients with at least one vaccination: 3
```

## 7. How to Run

1. Install Python 3.
2. Save the source code as `vaccination_tracker.py`.
3. Open a terminal in the folder.
4. Run:

```
python vaccination_tracker.py
```

## 8. Suggested GitHub Repository

Repository name: `oop1-vaccination-tracker`

```
oop1-vaccination-tracker/
├── vaccination_tracker.py
├── README.md
└── screenshots/
```

## 9. GitHub Submission

Create a GitHub repository, upload the Python file and README, and add the
lecturer as a collaborator according to the assignment instructions.

For the hardcopy, include screenshots showing the program source code and
successful program execution (see sections 10 and 11 below).

## 10. Source Code (`vaccination_tracker.py`)

```python
"""
OOP1 Assignment - Vaccination Tracker
PROG211: Object-Oriented Programming 1

Real-world domain: Health
Digital Public Goods (DPG) focus:
- Open-source
- Inclusive and accessible
- Privacy-respecting
- Modular and reusable
"""


class Patient:
    """Represents a patient using a non-sensitive identifier."""

    total_patients = 0

    def __init__(self, patient_id, name, age):
        self.patient_id = patient_id
        self.name = name
        self.age = age
        self.vaccinations = []
        Patient.total_patients += 1

    # Instance method
    def add_vaccination(self, vaccine_name, dose_number):
        """Add a vaccination record to this patient."""
        record = {
            "vaccine": vaccine_name,
            "dose": dose_number
        }
        self.vaccinations.append(record)

    # Instance method
    def display_info(self):
        """Display the patient's basic vaccination information."""
        print(f"Patient ID: {self.patient_id}")
        print(f"Name: {self.name}")
        print(f"Age: {self.age}")

        if self.vaccinations:
            print("Vaccinations:")
            for record in self.vaccinations:
                print(f"  - {record['vaccine']} (Dose {record['dose']})")
        else:
            print("Vaccinations: None")

    # Class method
    @classmethod
    def get_total_patients(cls):
        """Return the number of Patient objects created."""
        return cls.total_patients

    # Static method
    @staticmethod
    def is_valid_age(age):
        """Check whether an age is within a reasonable range."""
        return isinstance(age, int) and 0 <= age <= 120


class VaccinationCenter:
    """Represents a vaccination center."""

    def __init__(self, center_name, location):
        self.center_name = center_name
        self.location = location
        self.patients = []

    # Instance method
    def register_patient(self, patient):
        """Register a Patient object at this center."""
        self.patients.append(patient)

    # Instance method
    def display_patients(self):
        """Display all registered patients."""
        print(f"\nVaccination Center: {self.center_name}")
        print(f"Location: {self.location}")
        print("-" * 40)

        if not self.patients:
            print("No patients registered.")
            return

        for patient in self.patients:
            patient.display_info()
            print("-" * 40)

    # Class method
    @classmethod
    def from_default_location(cls, center_name):
        """Create a center using a default location."""
        return cls(center_name, "Freetown, Sierra Leone")

    # Static method
    @staticmethod
    def count_vaccinated(patients):
        """Count patients who have at least one vaccination."""
        return sum(1 for patient in patients if patient.vaccinations)


# Task 2: One data structure - a list of Patient objects.
def add_patient(patient_list, patient):
    """Add a Patient object to the list."""
    patient_list.append(patient)


def display_records(patient_list):
    """Display all patient records stored in the list."""
    print("\nALL PATIENT RECORDS")
    print("=" * 40)

    for patient in patient_list:
        patient.display_info()
        print("-" * 40)


# -------------------------
# Example program execution
# -------------------------
if __name__ == "__main__":
    # Validate ages before creating objects.
    if not Patient.is_valid_age(25):
        raise ValueError("Invalid age.")

    patient1 = Patient("P001", "Mariama", 25)
    patient2 = Patient("P002", "Mohamed", 8)
    patient3 = Patient("P003", "Fatmata", 31)

    # Interaction between objects and methods.
    patient1.add_vaccination("COVID-19", 1)
    patient1.add_vaccination("COVID-19", 2)

    patient2.add_vaccination("Measles", 1)
    patient2.add_vaccination("Polio", 1)

    patient3.add_vaccination("Tetanus", 1)

    # One list data structure storing multiple Patient objects.
    patients = []
    add_patient(patients, patient1)
    add_patient(patients, patient2)
    add_patient(patients, patient3)

    # Class method example.
    print("Total Patient Objects:", Patient.get_total_patients())
    # Create a vaccination center using a class method.
    center = VaccinationCenter.from_default_location("Central Vaccination Center")

    for patient in patients:
        center.register_patient(patient)

    center.display_patients()

    # Function using the list data structure.
    display_records(patients)

    # Static method example.
    vaccinated = VaccinationCenter.count_vaccinated(patients)
    print("Patients with at least one vaccination:", vaccinated)
```

### Source code screenshots

![Source code, lines 1-36](screenshots/01_source_lines_1-36.png)
![Source code, lines 13-68](screenshots/02_source_lines_13-68.png)
![Source code, lines 61-103](screenshots/03_source_lines_61-103.png)
![Source code, lines 103-138](screenshots/04_source_lines_103-138.png)
![Source code, lines 117-152](screenshots/05_source_lines_117-152.png)
![Source code, lines 138-161](screenshots/06_source_lines_138-161.png)

## 11. Successful Program Execution

Run in VS Code with Python 3.13 (`vaccination_tracker.py`), output shown in two parts:

![Program output, part 1](screenshots/07_output_part1.png)
![Program output, part 2](screenshots/08_output_part2.png)
