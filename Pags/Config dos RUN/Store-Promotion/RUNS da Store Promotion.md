[[Java]]  [[Pagbank]]

# LOCAL

## RUN/DEBUG CONFIGURATIONS


SPRING_PROFILES_ACTIVE=local,ap;
PORT=8080
## BANCO LOCAL MYSQL

### URL
	jdbc:mysql://localhost:3306/store_promotion
### USER
	root
### Sem password


# QA

DB_PASSWORD=store_promotionubrqa;
DB_USERNAME=store_promotionubr;
SPRING_PROFILES_ACTIVE=core, core_qa, qa, api

