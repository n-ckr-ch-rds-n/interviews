# Quiz Questions

##### Why are cache invalidation and naming things considered the hardest things in programming?
- I'm going to treat this as two questions: why is cache invalidation hard? and why is naming things hard?
- I don't know enough to know if these are really the hardest things in programming. I suspect not, but anyway...
- <strong>Cacheing First:</strong>  
- Cacheing is using a saved result from a previous computation in order to save time.
- Will the saved result work in the new computation? If not the cache must be ‘invalidated’.
- Working out the invalidation circumstances is what makes cache invalidation difficult.
- An example in Paella:
```
getAnimalNoise(animal) {
  makeCallToNoiseAPI(animal)
    .then(cacheResponse)
    .then(return Response)
}

getAnimalNoises(someanimals) {
  someanimals.forEachAnimal((animal => {
    if (animalNoiseIsCached) {
      return cachednoise(animal)
    } else {
      getAnimalNoise(animal)
    }
  }))
}
```
- Using the cached response saves time but do we always want the pig noise to be 'oink'? What if the user is from France where pigs say 'groin-groin'? What if we want the noise of a particular subspecies of pig that makes a different noise? We can't use the cached result...
- So we have to draw up a complicated set of rules for when it's ok to use the cached result and when it isn't. <strong>Hard!</strong>
*****
- <strong>Naming Things:</strong>
- Naming things well is important because other people will read your code and a good name communicates its intent.
- For example, naming a function getAnimalNoise() tells someone reading the code what the function is supposed to do.
- Naming things is hard because you might refer to a function or variable loads of times in you code before realising the name was bad. Changing lots of names is time-consuming and annoying and can introduce bugs.
- Sometimes functions are closely related but you don't want the names to be too similar.
- For example, in the above chunk of Paella I did naming badly (<em>intentionally</em>): getAnimalNoise() and getAnimalNoises() are too similar. But what to call them? <strong>Hard!</strong>


##### What is inversion control/dependency injection?
- It is a design pattern that aims to make chunks of code less dependent on each other.
- If you have two chunks of code, a and b, and a depends on b, you don't want to have to change a if you change b. Dependency injection makes it so you don't have to.
- Say I have two classes, a Wardrobe class that gets clothes from a database and a PersonalDresser class that recommends outfits...
- ... and the PersonalDresser works by invoking methods on the Wardrobe class as the Paella below illustrates:
```
chooseMySuit(styles) {
  var wardrobe = new Wardrobe;
  wardrobe.find(styles)
}
```
- This is not good if someone wants to use the PersonalDresser code but with a different kind of wardrobe. Maybe one that uses a completely different kind of database.
- Instead of making new instances of the Wardrobe class and calling its methods in the PersonalDresser methods, you can 'inject' the wardrobe class - any wardrobe class! - into the PersonalDresser class as one of its attributes.
- The Paella below imports a DiscoWardrobe class into PersonalDresser:
```
class PersonalDresser() {
  constructor(wardrobe = new DiscoWardrobe) {
    this.wardrobe = wardrobe;
  }
}
```
- This means that in the PersonalDresser class you can invoke methods of the DiscoWardrobe class like so:
```
PersonalDresser.prototype.chooseMySuit(styles) {
  this.wardrobe.find(styles)
}
```
- And you can insert any wardrobe with a find method into the PersonalDresser class!
```
class PersonalDresser() {
  constructor(wardrobe = new AstronautWardrobe) {
    this.wardrobe = wardrobe;
  }
}
```
- If you use a different kind of wardrobe you don't have to change all your PersonalDresser code. <strong>Nice!</strong>
- (Inversion Control is a really bad name for this technique. It is vague af. Dependency Injection is waaaaaay better.)

##### How does garbage collection work?
- Garbage collection is automatic memory management.
- The garbage collector frees up memory by removing unused values from their memory address spaces.
- It is useful to have garbage collectors because otherwise you would have to do your own memory management.
- i.e. You would have to remember where unused things were stored and delete them whenever there was a memory shortage.
- Low-level languages like C are like this. You have to free up memory yourself with commands like `free()`.
- In high-level languages like JavaScript the process is automatic.
- Assigning variables writes objects into memory. Objects are deleted by the garbage collector when not they're not referenced.  
- When the variable `a` is reassigned in the Paella example below, the object that used to be assigned to it is collected.
```
var a = { 'noise': 'baa' }
a = 1.3
```

##### How is a hash map implemented?
- A hashmap allocates an index to a key in a hash using a hash function.
- That sounds nuts. It makes more sense with an example:
- Say I have a key-value pair like `{ 'vodka': '45%' }` and I want to know its position in a hash that stores the percentage proof values for loads of alcoholic drinks.
- The hashmap can tell me where in the hash `{ 'vodka': '45%' }` is (if it's already in the hash), or where it should be inserted (if it's not). Index no. 25, for example.
- The hashmap does this with a 'hash function', a function that takes the key, (`'vodka'`), as an argument and returns an index.
- An issue with hash functions is that if they're not implemented well they can return the same index for different keys.
- Hash functions work out what the index of the key is based on rules. If the rules are faulty the function may return the same index for `'vodka'` as for `'gin'`. This is known as a 'hash collision'.
- A perfect hash function produces a 'uniform distrubution' of hash values, which is to say no collisions.
- Cryptographic functions are a good way of ensuring there are no collisions. Each key generates a unique index using encryption algorithms.   

##### What do you understand about usability principles? (for front end jobs)
What is the difference between a linked list and an array list?
Name a design pattern; how would you use it?
What does the Single Responsibility Principle mean?
What is encapsulation?
Why would you program using TDD? What are the drawbacks?
What do we mean by DRY?
What is MVC and why would we use it?
Describe classical vs. prototypical inheritance
What's the advantage of a no-sql database?
How would you deploy code to production?
What is a recent technical challenge you experienced and how did you solve it?
How do you debug?
What’s your process for using/learning about gems?
How would you go about getting up to speed at our company?
How would you build an API? What language would you use?
Why do companies increasingly move towards using micro services?
Have you ever used a grid system, and if so, what do you prefer?
What is CRUD?
What is the advantage in designing a RESTful API?
What are the benefits of a SQL database over other types of data-stores?
What’s the longest you’ve struggled on a problem?
What do you think about web sockets?
What does array inject do?
What’s wrong with the error message “undefined is not a function"?
What do we mean when we say Ruby is a human readable language?
What is the Principle of Least Astonishment?
What’s the difference between node and javascript
When should you raise exceptions?
What do we mean by prototypical inheritance?
How would you optimise a system that is running slow?
How would you identify bottlenecks in your system?
What is an 'n plus 1' problem?
How does the internet work?
What do you understand by estimation? (e.g. planning poker, T-shirt sizing) How would you work out how long something would take?
