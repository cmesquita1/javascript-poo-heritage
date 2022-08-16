# Assessment - Extend Oregon Trail with Inheritance

Recall how to use inheritance/delegation to extend a class object, creating a new variation on the original class. Here's an example:

```js
function Dog (name, breed, isGoodBoy) {
    this.name = name;
    this.breed = breed;
    this.isGoodBoy = isGoodBoy;
}

Dog.prototype.sit = function () {
        // sitting code here
}

function GuardDog (name, breed, isGoodBoy, attackWord) {
    Dog.call(this, name, breed, isGoodBoy);
    this.attackWord = attackWord;
}
GuardDog.prototype = Object.create(Dog.prototype);
GuardDog.prototype.constructor = GuardDog;

GuardDog.prototype.bark = function () {
    // barking code here
}

```
For this assessment you will extend your Oregon Trail code to use inheritance to create two new
types of traveler: `Doctor` and `Hunter`. They will have all of the features of any other `Traveler`,
but with these differences:

A `Doctor` is a `Traveler` with one additional method:

### Doctor.prototype.heal(traveler)
Pass another `Traveler` as a parameter to the `.heal()` method, and their `isHealthy` property
is changed to true.

A `Hunter` is a `Traveler` that is better at finding food, but requires more food to eat. They should
start out with 2 food instead of just 1 like other travelers do. They can
also give food to other travelers:

### Hunter.prototype.hunt()
Increase the hunter's food by 5. (A normal traveler gains only 2.)

### Hunter.prototype.eat()
Consumes 2 units of the hunter's food. If the hunter doesn't have 2 food when they are instructed to eat, they eat as much as they can (0 or 1 unit), but the hunter is no longer healthy. (A normal traveler eats only 1 unit of food.)

### Hunter.prototype.giveFood(traveler, numOfFoodUnits)
Transfers `numOfFoodUnits` from the hunter to a different traveler. If the hunter has less food than they are being asked to give, then no food should be transferred.

## Testing
Replace the testing code at the end of your original Oregon Trail implementation
with this new testing code to verify that it is working properly. (Don't modify this code!)

```js
// Create a wagon that can hold 4 people
let wagon = new Wagon(4);
// Create five travelers
let henrietta = new Traveler('Henrietta');
let juan = new Traveler('Juan');
let drsmith = new Doctor('Dr. Smith');
let sarahunter = new Hunter('Sara');
let maude = new Traveler('Maude');

console.log(`#1: There should be 4 available seats. Actual: ${wagon.getAvailableSeatCount()}`);

wagon.join(henrietta);
console.log(`#2: There should be 3 available seats. Actual: ${wagon.getAvailableSeatCount()}`);

wagon.join(juan);
wagon.join(drsmith);
wagon.join(sarahunter);

wagon.join(maude); // There isn't room for her!
console.log(`#3: There should be 0 available seats. Actual: ${wagon.getAvailableSeatCount()}`);

console.log(`#4: There should be 5 total food. Actual: ${wagon.totalFood()}`);

sarahunter.hunt(); // gets 5 more food
drsmith.hunt();

console.log(`#5: There should be 12 total food. Actual: ${wagon.totalFood()}`);

henrietta.eat();
sarahunter.eat();
drsmith.eat();
juan.eat();
juan.eat(); // juan is now hungry (sick)

console.log(`#6: Quarantine should be true. Actual: ${wagon.shouldQuarantine()}`);
console.log(`#7: There should be 7 total food. Actual: ${wagon.totalFood()}`);

drsmith.heal(juan);
console.log(`#8: Quarantine should be false. Actual: ${wagon.shouldQuarantine()}`);

sarahunter.giveFood(juan, 4);
sarahunter.eat(); // She only has 1, so she eats it and is now sick

console.log(`#9: Quarantine should be true. Actual: ${wagon.shouldQuarantine()}`);
console.log(`#10: There should be 6 total food. Actual: ${wagon.totalFood()}`);

```
