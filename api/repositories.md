---
description: Configuring repositories in Konstrukt, the fluent administration panel builder for Umbraco.
---

# Repositories

Repositories are used by Konstrukt to access the entity data stores. By default, collections will use a generic built in PetaPoco repository however you can define your own repository implementation should you wish to store your entities via an alternative strategy.

## Defining a repository

To define a repository you create a class that inherits from the base class `KonstruktRepository<TEntity, TId>` and implements all of its abstract methods.

````csharp
// Example
public class PersonRepository : KonstruktRepository<Person, int> {

    protected override int GetIdImpl(Person entity) {
        return entity.Id;
    }

    protected override Person GetImpl(int id) {
        ...
    }

    protected override IEnumerable<Person> GetAllImpl() {
        ...
    }

    protected override PagedResult<Person> GetPagedImpl(int pageNumber, int pageSize, Expression<Func<Person, bool>> whereClause, Expression<Func<Person, object>> orderBy, SortDirection orderDirection) {
        ...
    }

    protected override Person SaveImpl(Person entity) {
        ...
    }

    protected override void DeleteImpl(int id) {
        ...
    }

    protected override long GetTotalRecordCountImpl() {
        ...
    }
}
````

**Note:** For all `Impl` methods there are public alternatives without the `Impl` suffix, however we have separate implementation methods in order to ensure all repositories fire the relevant Konstrukt events whether triggered via the Konstrukt UI or not.

## Defining a child repository

To define a repository for a child collection you create a class that inherits from the base class `KonstruktChildRepository<TEntity, TId, TFk>` and implements all of the same abstract methods of the `KonstruktRepository<TEntity, TId>` class as defined above, along with the following additional methods.

````csharp
// Example
public class ChildRepository : KonstruktChildRepository<Child, int, int> {

    ...

    protected int GetForeignKeyImpl(Child entity){
        return entity.ParentId;
    }

    protected IEnumerable<Child> GetAllImpl(int foreignKey) {
        ...
    }

    protected long GetTotalRecordCountImpl(int foreignKey) {
        ...
    }
}
````

## Changing the repository implementation of a collection

A repository is assigned to a collection as part of the collection configuration. See [Collection API Documentation](collections.md#changing-a-collection-repository-implementation) for more info.

## Accessing a repository in code

If you have created your own repository implementation, then accessing the repository can be as simple as instantiating a new instance of the repository class, however if you are using the built in repository, unfortunately a new instance can't be created in this way.

To help with accessing a repository (default or custom) Konstrukt has a `IKonstruktRepositoryFactory` you can inject into your code base with a couple of factory methods to create the repository instances for you.

#### **IKonstruktRepositoryFactory.GetRepository&lt;TEntity, TId&gt;() : KonstruktRepository&lt;TEntity, TId&gt;**

Creates a repository for the given entity type. Konstrukt will search the configuration for the first section / collection with a configuration for the given entity type and use that as repository configuration.

````csharp
// Example
public class MyController : Controller
{
    private readonly KonstruktRepository<Person, int> _repo;

    public MyController(IKonstruktRepositoryFactory repoFactory) 
    {
        _repo = repoFactory.GetRepository<Person, int>();
    }
}
````

#### **IKonstruktRepositoryFactory.GetRepository&lt;TEntity, TId&gt;(string sectionAlias, string collectionAlias) : KonstruktRepository&lt;TEntity, TId&gt;**

Creates a repository for the given entity type from the given section / collection configuration.

````csharp
// Example
public class MyController : Controller
{
    private readonly KonstruktRepository<Person, int> _repo;

    public MyController(IKonstruktRepositoryFactory repoFactory) 
    {
        _repo = repoFactory.GetRepository<Person, int>("repositories", "person");
    }
}
````

