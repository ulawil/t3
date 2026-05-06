* Novice
  * [ ] ORM purpose, pros & cons
  * [x] Session vs entity manager
  * [x] Entity states
  * [ ] Basic types mapping
  * [ ] Session methods: update vs merge, save vs persist, flush, saveOrUpdate
  * [ ] Assosiation types, persisting collections, maps. @JoinColumn annotation
  * [ ] Cascade operations
  * [ ] Entity listeners & JPA callbacks
  * [ ] N + 1 problem, ways to resolve
  * [ ] @GeneratedValue, generation strategies.
* Competent
  * [ ] IdentityMap, UnitOfWork patterns 
  * [ ] Active record/data mapper patterns
  * [ ] Queries caching, restrictions, cache modes, best practices. Cache levels.
  * [x] Bulk operations
  * [ ] Lazy loading / Eager loading; Extra lazy collections fetching
  * [ ] HQL vs JPQL
  * [ ] Native queries, named native queries
  * [ ] @Transient, use cases
  * [ ] @MappedSuperclass, inheritance mapping, inheritance mapping types, pros & cons
  * [ ] Criteria API

# Session vs entity manager
- EntityManager - JPA interface that represents persistence context/1st level cache; implementation needs to be provided by the persistence provider, e.g Hibernate
- Session - Hibernate interface that represents persistence context + implementation;

# Entity states
- Transient - entity is not associated with persistence context and does not have a corresponding table row 
- Persistent - entity is associated with persistence context and has or will have a corresponding table row once the session is flushed
- Detached - entity is no longer associated with persistence context but has a corresponding table row
- Removed - entity is associated with persistence context but is marked for removal

# Bulk operations
```yaml
# set to enable bulk operations:
spring:
  jpa:
    properties:
      hibernate: 
        batch_size: ...
        # a batch cannot contain more than one entity type, so if inserting/updating multiple types, set
        order_inserts: true
        order_updates: true
```
