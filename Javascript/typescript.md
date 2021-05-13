```javascript
type PokemonVariation = 'water' | 'fire' | 'grass' | 'ice' | 'bug' | 'ground' | 'electric' | 'flying' | 'psychic' | 'dark' | 'ghost';

interface PokemonType {
    typeWeakness: PokemonVariation[];
    typeResiliant: PokemonVariation[];
    typeEffective: PokemonVariation[];
}

class Pokemon {
    name: string;
    type: PokemonType;

    constructor(name, type: PokemonType) {
        this.name = name;
        this.type = type;
    }
}

const FireType: PokemonType = {
  typeWeakness: ['water', 'ground'],
  typeResiliant: ['fire', 'grass'],
  typeEffective: ['grass']
}

const Charmander = new Pokemon('Charmander', FireType);

console.log(Charmander.type.typeWeaknesses); // ['water', 'ground']
```