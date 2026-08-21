# Restful Booker API Testing Project

**API under test:** [https://restful-booker.herokuapp.com](https://restful-booker.herokuapp.com)
**Team:** Restful-Booker Team — Farah Talalweh, **Sahar Dwaikat**, Samir Qumri
**Methodology:** Scrum, 5-day sprint
**My role:** QA Engineer — owned **GET /booking** (retrieval & filtering) and
**PUT/PATCH /booking/:id** (full & partial updates), and consolidated the team's test
case matrix, defect log, and Requirements Traceability Matrix (RTM).

## About This Project

This was a 3-person QA team project testing the full Restful Booker API — authentication,
booking CRUD, and health checks — combining manual test design (Excel test case matrix, RTM,
defect log) with Postman-based execution and a Python/pytest automation layer.

This repo preserves the team's original deliverables and adds an automated regression suite on
top of them, mapping each automated test back to its Requirement ID, Test Case ID, and (where
applicable) Defect ID.

## My Contribution

| Area | Details |
|---|---|
| Test design & execution | Designed and ran positive/negative/boundary test cases for `GET /booking` and `PUT/PATCH /booking/:id` |
| Defect reporting | Authored 5 of the 18 logged defects (DEF-001 through DEF-005), all on retrieval/update behavior |
| Documentation | Consolidated the team's Excel test case matrix, defect log, and RTM |
| Automation | Wrote the pytest automation layer (`tests/`) covering all endpoints, translating the team's Excel test cases into executable regression tests |

## Test Results Summary (manual execution, per team Summary Report)

| Metric | Value |
|---|---|
| Total test cases | 97 |
| Passed | 67 (69%) |
| Failed | 30 (31%) |
| Total defects logged | 18 (7 High, 8 Medium, 3 Low) |

Full breakdown by module is in `docs/Restful_Booker__Test_cases___bug_report___Updated.xlsx`
(Summary Report tab).

## Project Structure

```
restful-booker-api-testing/
├── tests/
│   ├── conftest.py              # shared fixtures: base URL, auth token, booking factory
│   ├── test_ping.py             # health check
│   ├── test_auth.py             # POST /auth
│   ├── test_booking_retrieval.py # GET /booking, GET /booking/{id}  ← my ownership area
│   ├── test_booking_update.py    # PUT/PATCH /booking/{id}          ← my ownership area
│   ├── test_booking_create.py   # POST /booking
│   └── test_booking_delete.py   # DELETE /booking/{id}
├── postman/
│   ├── Sahar.postman_collection.json      # my individual Postman collection
│   ├── Farah.postman_collection.json      # teammate's collection (Auth + Ping)
│   └── Samir's TCs.postman_collection.json # teammate's collection (Ping + Delete)
├── docs/
│   ├── Test_Plan_Restful_Booker_API_EN.docx
│   ├── Restful_Booker__Test_cases___bug_report___Updated.xlsx
│   └── Restful_Booker_RTM.xlsx
├── .github/workflows/run-tests.yml
├── requirements.txt
└── README.md
```

## How Known Bugs Are Handled in Automation

Where the team's manual testing found a real defect (e.g. `DEF-007`: DELETE returns `201`
instead of `204`), the corresponding automated test asserts the **correct, documented**
behavior and is marked `@pytest.mark.xfail(reason="DEF-00X: ...")`. This means:

- The suite stays green in CI even though the underlying bug is still open
- If the bug is ever fixed upstream, that test flips to `XPASS`, flagging it for a status update
- Anyone reading the test file immediately sees which behaviors are known-broken and why

## How to Run the Automated Tests

```bash
pip install -r requirements.txt
pytest -v
```

With an HTML report:

```bash
pytest -v --html=report.html --self-contained-html
```

## How to Use the Postman Collections

1. Open Postman
2. Import any of the `.json` files in `postman/`
3. Run with the Collection Runner, or via CLI with Newman:
   ```bash
   newman run "postman/Sahar.postman_collection.json"
   ```

## About Me

Aspiring QA Engineer with hands-on training in manual and automation testing from an intensive
QA bootcamp. Background includes 9+ years of professional experience in process optimization,
systems implementation, and cross-functional collaboration. PMP-certified.

[LinkedIn](https://linkedin.com/in/sahardwaikat) | sahar.dwaikat@gmail.com
