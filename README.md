openapi: 3.0.3
info:
  title: Settlement API
  version: 1.0.0
  description: API to create a settlement record with either a details array or cache management object.

paths:
  /settlement:
    post:
      summary: Create a settlement
      description: Creates a new settlement. The details object can either contain an array of entries or a single cache management object.
      requestBody:
        required: true
        content:
          application/json:
            schema:
              type: object
              properties:
                settlement:
                  type: object
                  properties:
                    settlementId:
                      type: string
                      example: "SETT-20251031-001"
                    details:
                      oneOf:
                        - type: object
                          properties:
                            entries:
                              type: array
                              description: List of settlement entries
                              items:
                                type: object
                                properties:
                                  transactionId:
                                    type: string
                                    example: "TXN-001"
                                  amount:
                                    type: number
                                    format: double
                                    example: 2500.75
                                  currency:
                                    type: string
                                    example: "INR"
                          required:
                            - entries
                        - type: object
                          properties:
                            cacheManagement:
                              type: object
                              description: Cache management details for settlement
                              properties:
                                cacheId:
                                  type: string
                                  example: "CACHE-98765"
                                lastUpdated:
                                  type: string
                                  format: date-time
                                  example: "2025-10-31T12:30:00Z"
                          required:
                            - cacheManagement
                  required:
                    - settlementId
                    - details
      responses:
        '201':
          description: Settlement created successfully
          content:
            application/json:
              schema:
                type: object
                properties:
                  message:
                    type: string
                    example: "Settlement created successfully"
                  settlementId:
                    type: string
                    example: "SETT-20251031-001"
        '400':
          description: Invalid input
