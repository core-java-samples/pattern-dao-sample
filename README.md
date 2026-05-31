# pattern-dao-sample

A minimal demonstration of the DAO (Data Access Object) pattern in Java.

## What It Demonstrates

DAO is a pattern that hides data access details behind an interface. 

Business logic works against the `UserRepository` interface and has no knowledge of where or how data is stored — whether in a HashMap, ArrayList, PostgreSQL, or anything else.

The project illustrates this with a concrete example: the same `UserRepository` interface is implemented two ways — via `HashMap` and via `ArrayList`. Behavior is identical, implementation is different.

## Structure

All code is in a single file: `DaoArchitecture.java`

```
DaoArchitecture.java
│
├── User                          # Model — record with id and name
├── UserRepository                # DAO contract — findById / findAll / save / delete
├── InMemoryMapUserRepository     # Implementation via HashMap — O(1) lookup by id
├── InMemoryListUserRepository    # Implementation via ArrayList — sequential scan O(n)
└── DaoArchitecture               # Entry point + demo()
```

## Key Points

**Interface as contract.** `UserRepository` defines what to do — not how. The calling code is written against the interface and has no idea which implementation is in use.

**Two implementations — one behavior.** `InMemoryMapUserRepository` uses a `HashMap` — O(1) lookup by id. `InMemoryListUserRepository` uses an `ArrayList` — sequential scan at O(n). From the outside, there is no difference.

**Substitutability.** Swapping the implementation requires changing a single line. Nothing else changes — that is the point of DAO.

## Console Output

```
MAP:  Optional[User[id=1, name=jack]]
LIST: Optional[User[id=1, name=jack]]
```

Both implementations return the same result.

## Run

```bash
./mvnw spring-boot:run
```

## See also

- Next: [in-memory-repository-sample](https://github.com/core-java-samples/in-memory-repository-sample)
