# SmartRetail P5 – Similar Product Finder - Group 5

## 1. Group Members

| Name | GitHub username | Role |
|-|-|-|
| Đặng Hoàng Minh Anh | minhanhhOvO | Leader |
| Phan Công Tấn Đạt | phancongtandat | Member |
| Nguyễn Minh Hùng | HungNguyen12101 | Member |
| Đặng Anh Khôi | TonyDang08 | Member |

Lecturer: Lê Văn Thể - vvvanthe

## 2. Problem specification
Find products similar to the one a customer likes, taking in-store stock into account, and print the Top-K.

- **Input:** `products.csv`, `inventory.csv`, and `p5 <data_folder> <product_id> [store_id] [K] [max_price] [--brand <brand>] [--export <file.csv>]`.
- **Processing:** skip invalid lines with a warning and line number on `cerr`; report a clear error for bad arguments or a missing file; filter by max price and `--brand`; score similarity (category +4, brand +3, price within 20% +2, rating within 0.3 +1); adjust by stock (0 gives −5, 1–2 gives 0, 3 or more gives +1); sort by final score, then similarity, rating and `product_id`.
- **Output:** `QUERY` line, full table, Top-K with reasons and stock labels (other stores with stock for out-of-stock items), rank-drop note, `BEST SUBSTITUTE BY STORE`, and the number of products excluded by max price. Optional `--export` writes the Top-K to CSV.

## 3. Build and run
```bash
mkdir -p bin
g++ -std=c++17 -Wall -Wextra src/main.cpp -o bin/p5
./bin/p5 data/sample P001
./bin/p5 data/full P001 S002 3 4000000
```
## 4. Assumptions and limitations
- A product with no stock line in the current store is treated as `stock = 0`.
- Rating is stored as integer tenths and the 20% price rule uses cross-multiplication, so `double` is never compared at the boundaries.
- Boundaries are strict `<`; a product priced exactly at the max price is kept.
- Duplicate keys: the first line is kept.
- `--brand` is an exact, case-sensitive match.

## 5. What this project does NOT do

- P5 only reads stock for ranking. It does not classify stock alerts and does not compute orders.
- It does not modify `products.csv` or `inventory.csv`.
- It does not use classes, pointers, `new/delete`, inheritance, `map/set`, exceptions, templates, lambdas or `std::sort`.

## 6. Task assignment table
| ID | Task | Function / file | Assignee | Reviewer | Flowchart | PR |
|-|-|-|-|-|-|-|
| T01 | struct and change rating | `Product`, `StockItem`, `Match`, `toTenths()` | Khôi | Hùng | yes | # |
| T02 | Read products.csv and check error | `loadProducts()` | Hùng | Đạt | yes | # |
| T03 | Read inventory.csv and check error | `loadInventory()` | Anh | Hùng | yes | # |
| T04 | Search functions, find query product, look up stock | `findProduct()`, `stockOf()` | Đạt | Hùng | yes | # |
| T05 | Sort products by id | `sortProductsById()` | Hùng | Anh | yes | # |
| T06 | Compare and sort matches | `comesBefore()`, `sortMatches()` | Hùng | Anh | yes | # |
| T07 | Similarity score and reasons | `similarity()` **(hàm lõi)** | Đạt | Khôi | yes | # |
| T08 | Stock adjustment and other stores | `availabilityAdjustment()`, `availableElsewhere()` | Anh | Đạt | yes | # |
| T09 | Filter, score, rank | `rankMatches()` | Khôi | Đạt | yes | # |
| T10 | Print full table | `printReport()` | Khôi | Anh | yes | # |
| T11 | Print Top-K | `printTopK()` | Anh | Khôi | yes | # |
| T12 | Best substitute by store | `printBestSubstitutes()` | Anh | Hùng | yes | # |
| T13 | Command-line arguments and main flow | `main()` | Đạt | Khôi | yes | # |
| T14 | (Optional) Export Top-K to CSV | `--export` | Hùng | Anh | yes | # |
| T15 | Repo skeleton | `.gitignore`, `.github/pull_request_template.md`, `data/` | Hùng | Anh | not needed | #2 |
| T16 | Task assignment table | `README.md` | Anh | Hùng | not needed | #3 |
| T17 | Test cases table | `tests/test_cases.md` | Khôi | Đạt | not needed | # |
| T18 | Expected outputs and test script | `tests/expected/`, `tests/run_tests.sh` | Anh | Hùng | not needed | # |
| T19 | Architecture | `docs/architecture.md` | Hùng | Khôi | not needed | # |
| T20 | Slides | `docs/slides.pdf` | Đạt | Anh | not needed | # |
| T21 | Setup GitHub repo | GitHub Settings | Anh | - | not needed | - |
| T22 | Final checklist and tag final | `git tag final` | Anh | - | not needed | - |
| T23 | Complete README sections & final AI declaration | `README.md` | Anh | Đạt | not needed | # | 
## 7. AI declaration

| Tool | Used for | Part of the project |
|-|-|-|
| Claude | List and distribute tasks equally among members | T16: Task assignment table |
| ChatGPT | Empty folders didn't get added? | T15: Repo Skeleton |
