OpenAPI 3.1 では **JSON Schema 2020-12** が完全にサポートされています。これにより、OpenAPI 3.0 にはなかったより豊富な表現力でスキーマ定義が可能になりました。以下、**OpenAPI 3.1**でのJSON Schema定義方法の詳細と具体例を紹介します。

---

## 1. **基本構造（OpenAPI 3.1）**

```yaml
openapi: 3.1.0
info:
  title: Example API
  version: 1.0.0
paths:
  /users:
    post:
      summary: Create a new user
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/User'
      responses:
        '201':
          description: User created successfully
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/User'
components:
  schemas:
    User:
      $schema: "https://json-schema.org/draft/2020-12/schema"
      type: object
      required:
        - id
        - name
        - email
      properties:
        id:
          type: integer
          example: 1
        name:
          type: string
          example: "Alice"
        email:
          type: string
          format: email
          example: "alice@example.com"
        age:
          type: integer
          minimum: 0
          maximum: 120
        preferences:
          type: object
          properties:
            notifications:
              type: boolean
              default: true
            theme:
              type: string
              enum: ["light", "dark"]
              example: "dark"
        address:
          type: object
          properties:
            street:
              type: string
            city:
              type: string
            postalCode:
              type: string
          required: [street, city]
```

---

## 2. **OpenAPI 3.1 の特徴と改善点**  
### (1) **JSON Schemaとの互換性**
- OpenAPI 3.1 は JSON Schema 2020-12 に完全準拠しているため、JSON Schema の全機能（`if/then/else`などの条件付きスキーマ、`$schema`参照など）が利用できます。

### (2) **コンポーネントのスキーマに `$schema`**
- `$schema` を使うことで、スキーマがどのバージョンの JSON Schema に基づいているかを明示できます。

---

## 3. **新しい JSON Schema の要素**

### (1) **`if/then/else` 条件付きスキーマ**
以下の例では、ユーザーの年齢に応じてオプションフィールドのバリデーションを変更しています。

```yaml
components:
  schemas:
    User:
      type: object
      properties:
        age:
          type: integer
        guardianName:
          type: string
      if:
        properties:
          age:
            maximum: 17
      then:
        required: ["guardianName"]
```

**解説:**  
- 年齢が17歳以下の場合、`guardianName` が必須になります。

---

### (2) **`oneOf` / `anyOf` / `allOf` の使用**  
複雑なデータ構造の表現も可能です。

```yaml
Pet:
  type: object
  properties:
    petType:
      type: string
  required: ["petType"]
  oneOf:
    - properties:
        petType:
          const: "Dog"
        breed:
          type: string
          example: "Golden Retriever"
    - properties:
        petType:
          const: "Cat"
        declawed:
          type: boolean
          example: true
```

**解説:**  
- `petType` が `Dog` の場合は `breed` を指定、`Cat` の場合は `declawed` を指定するようにバリデーションされます。

---

## 4. **OpenAPI 3.1 におけるエンドポイントの記述例**

```yaml
paths:
  /pets:
    get:
      summary: Get list of pets
      responses:
        '200':
          description: List of pets
          content:
            application/json:
              schema:
                type: array
                items:
                  $ref: '#/components/schemas/Pet'
```

この例では、`/pets` エンドポイントにアクセスすると、`Pet` オブジェクトの配列が返されることを示しています。

---

## 5. **OpenAPI 3.1 の使用上のポイント**

- **互換性に注意**: OpenAPI 3.1 で生成した API 定義は、3.0 対応のツール（例: 一部の古い Swagger ツール）では利用できない場合があります。
- **最新ツールの使用**: `Swagger UI` などのツールも、最新バージョンで 3.1 をサポートしていることを確認する必要があります。

---

## 6. **まとめ**

OpenAPI 3.1 では、JSON Schema 2020-12 に準拠することで、より強力なバリデーションと柔軟なスキーマ定義が可能になりました。特に、`if/then/else` や `oneOf` のような高度なスキーマ表現を活用することで、複雑なデータモデルの記述も容易です。

もし特定のスキーマやユースケースに合わせた例が必要であればお知らせください！