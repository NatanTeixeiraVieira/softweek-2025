# Sistema de gerenciamento de estoque

## Regras

- Preço do produto não pode ser maior do que R$ 5.000,00
- O nome do produto precisa conter pelo menos 3 caracteres

## FileProductRepository

```
  import { promises as fs } from "fs";
  import { join } from "path";


  // findById

   try {
      const data = await fs.readFile(DATA_FILE, "utf-8");
      const products = data ? JSON.parse(data) : [];
      const found = products.find((p: any) => p.id === id);
      if (!found) return null;
      // Ajuste conforme o construtor da sua entidade Product
      return new Product(found);
    } catch (err) {
      if ((err as NodeJS.ErrnoException).code === "ENOENT") {
        return null;
      }
      throw err;
    }


  // create

   let products: any[] = [];
    try {
      const data = await fs.readFile(DATA_FILE, "utf-8") ;
      products = data ? JSON.parse(data) : [] ;
    } catch (err) {
      if ((err as NodeJS.ErrnoException).code !== "ENOENT") {
        throw err;
      }
    }


    products.push(product.toJSON());

    await fs.writeFile(DATA_FILE, JSON.stringify(products, null, 2), "utf-8");


    // update

    let products: any[] = [];
    try {
      const data = await fs.readFile(DATA_FILE, "utf-8");
      products = data ? JSON.parse(data) : [];
    } catch (err) {
      if ((err as NodeJS.ErrnoException).code !== "ENOENT") {
        throw err;
      }
    }

    const index = products.findIndex((p: any) => p.id === product.id);
    if (index === -1) {
      throw new Error(`Product with id ${product.id} not found.`);
    }

    products[index] = product.toJSON();

    await fs.writeFile(DATA_FILE, JSON.stringify(products, null, 2), "utf-8");

```
