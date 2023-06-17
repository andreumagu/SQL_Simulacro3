# Simulacro 3 SQL

1. Muestra todas las piezas que sean de color rojo.

    ```sql
    SELECT *
    FROM Piezas
    WHERE color = 'rojo';
    ```

2. Muestra todos los proveedores que estén ubicados en la ciudad de 'Madrid'.

    ```sql
    SELECT nombre_proveedor
    FROM Proveedores
    WHERE ciudad_proveedor = 'Madrid';
    ```

3. Muestra el nombre de la pieza más pesada.

    ```sql
    SELECT nombre_pieza
    FROM piezas
    ORDER BY Peso DESC
    LIMIT 1;
    ```

4. Muestra el nombre del proveedor que suministra la mayor cantidad de piezas diferentes.

    ```sql
    SELECT nombre_proveedor
    FROM proveedores
    WHERE id_proveedor IN (
        SELECT id_proveedor
        FROM Piezas
        GROUP BY id_proveedor
        ORDER BY COUNT(id_pieza) DESC
    )
    LIMIT 1;
    ```

    ![4](/img/4.png)

5. Saca todos los proveedores que suministren al menos una pieza de color azul.

    ```sql
    SELECT nombre_proveedor
    FROM Proveedores
    WHERE id_proveedor IN (
        SELECT id_proveedor
        FROM Piezas
        WHERE color = 'Azul'
        GROUP BY id_proveedor
    );
    ```

6. Visualiza el nombre de la pieza más ligera que es suministrada por el proveedor 'Proveedor A'.

    ```sql
    SELECT Piezas.nombre_pieza
    FROM Piezas
    INNER JOIN Proveedores ON Piezas.id_proveedor = Proveedores.id_proveedor
    WHERE Proveedores.nombre_proveedor = 'Proveedor A' AND Piezas.peso = (
        SELECT MIN(peso)
        FROM Piezas
    );
    ```

7. Saca el nombre del proveedor que suministra la pieza más pesada.

    ```sql
    SELECT Proveedores.nombre_proveedor
    FROM Proveedores
    INNER JOIN Piezas ON Proveedores.id_proveedor = Piezas.id_proveedor
    WHERE peso = (
        SELECT MAX(peso)
        FROM Piezas
    );
    ```

    ![7](/img/7.png)

8. Muestra todas las piezas que sean suministradas por proveedores de la ciudad de Barcelona'.

    ```sql
    SELECT *
    FROM Pieras
    INNER JOIN Proveedores ON Piezas.id_proveedor = Proveedores.id_proverdor
    WHERE Proveedores.ciudad_proveedor = 'Barcelona';
    ```

9. Muestra el nombre del proveedor que suministra la mayor cantidad de piezas de
color verde.

    ```sql
    SELECT Proveedores.nombre_proveedor
    FROM Proveedores
    WHERE id_proveedor IN (
        SELECT proveedor, COUNT(id_pieza) As rec
        FROM Piezas
        WHERE color = 'Verde'
        ORDER BY rec DESC
        GROUP BY id_proveedor
        LIMIT 1
    );
    ```

10. Muestra el nombre de la pieza más pesada que es suministrada por un proveedor de la ciudad de Valencia.

    ```sql
    SELECT Piezas.nombre_pieza
    FROM Piezas
    INNER JOIN Proveedores ON Piezas.id_proveedor = Proveedores.id_proveedor
    WHERE Pieza.peso = MAX (Pieza.peso) AND Proveedores.ciudad_proveedor =
    'Valencia';
    ```
