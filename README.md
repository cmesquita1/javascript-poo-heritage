# Entrega - Estendendo o Oregon Trail com Herança

Para iniciar, faça o clone desse repositório.

Relembre como usar herança/delegação para estender um objeto de classe criando uma nova variação da classe original. Aqui está um exemplo:

```js
class Dog {
   constructor(name, breed, isGoodBoy) {
      this.name = name;
      this.breed = breed;
      this.isGoodBoy = isGoodBoy;
   }

   sit() {
       // sitting code here
   }
}
 
class GuardDog extends Dog {
   constructor(name, breed, isGoodBoy, attackWord) {
      super(name, breed, isGoodBoy)
      this.attackWord = attackWord;
   }

   bark() {
      // barking code here
   }
}
```

Nesta Entrega, você irá estender seu código do Oregon Trail para usar herança para criar dois novos tipos de viajantes: `Hunter` (Caçador) e `Doctor` (Médico). Eles terão todas as outras características de qualquer outro Viajante, com essas diferenças:

## Hunter

Um Caçador é um Viajante que se dá melhor encontrando comida, mas também precisa de mais comida. Ele começa com 2 comidas em vez de apenas 1 como os outros viajantes. Ele também pode dar comida para outros viajantes:

### Método hunt()

Aumente a comida do caçador em 5. (Um viajante convencional ganha apenas 2.)

### Método eat()

Consome 2 unidades da comida do caçador. Se um caçador não tiver 2 comidas quando for instruído a comer, ele come o quanto puder (0 ou 1 unidade), mas o caçador não fica mais saudável. (Um viajante normal come apenas 1 unidade de comida.)

### Método giveFood(traveler, numOfFoodUnits)

Transfere numOfFoodUnits do caçador para outro viajante. Se o caçador tiver menos comida do que foi instruído a dar, então nenhuma comida é transferida.

## Doctor

Um médico é um viajante que se dá melhor curando outros viajantes, como médico ele deve curar outros viajantes para que eles possam seguir a viagem saudável. Ele possui apenas um método.

### Método heal(traveler)

Este método cura viajantes doentes fazendo com que eles sigam viagem saudáveis.Nesta etapa um viajante será passado como parâmetro para o método .heal(), para viajantes doentes, a propriedade isHealthy do viajante deverá mudar para true. Para viajantes que não estão doentes a saúde do mesmo, deve continuar como verdadeiro

## Teste

Substitua o código de teste no final da sua implementação original de Oregon Trail por este novo código de teste para verificar se ele está funcionando apropriadamente. (Não modifique este código!)

```js
// Cria uma carroça que comporta 4 pessoas
let wagon = new Wagon(4);
// Cria cinco viajantes
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
 
wagon.join(maude); // Não tem espaço para ela!
console.log(`#3: There should be 0 available seats. Actual: ${wagon.getAvailableSeatCount()}`);
 
console.log(`#4: There should be 5 total food. Actual: ${wagon.totalFood()}`);
 
sarahunter.hunt(); // pega mais 5 comidas
drsmith.hunt();
 
console.log(`#5: There should be 12 total food. Actual: ${wagon.totalFood()}`);
 
henrietta.eat();
sarahunter.eat();
drsmith.eat();
juan.eat();
juan.eat(); // juan agora está doente (sick)
 
console.log(`#6: Quarantine should be true. Actual: ${wagon.shouldQuarantine()}`);
console.log(`#7: There should be 7 total food. Actual: ${wagon.totalFood()}`);
 
drsmith.heal(juan);
console.log(`#8: Quarantine should be false. Actual: ${wagon.shouldQuarantine()}`);
 
sarahunter.giveFood(juan, 4);
sarahunter.eat(); // Ela só tem um, então ela come e fica doente
 
console.log(`#9: Quarantine should be true. Actual: ${wagon.shouldQuarantine()}`);
console.log(`#10: There should be 6 total food. Actual: ${wagon.totalFood()}`);
```

## Envio

Faça o push do código para o seu repositório GitHub e implemente-o via GitHub pages. No Canvas, envie a url do seu GitHub pages (por exemplo https://username.github.io/oregon-trail-inheritance/)
