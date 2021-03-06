# Migration `20200803235103`

This migration has been generated by Anand Chowdhary at 8/3/2020, 11:51:03 PM.
You can check out the [state of the schema](./schema.prisma) after the migration.

## Database Steps

```sql
CREATE TABLE `staart`.`users` (
`checkLocationOnLogin` boolean NOT NULL DEFAULT false,
`countryCode` varchar(191) NOT NULL DEFAULT 'us',
`createdAt` datetime NOT NULL DEFAULT CURRENT_TIMESTAMP,
`gender` ENUM('MALE', 'FEMALE', 'NONBINARY', 'UNKNOWN') NOT NULL DEFAULT 'UNKNOWN',
`id` int NOT NULL  AUTO_INCREMENT,
`name` varchar(191) NOT NULL ,
`notificationEmails` ENUM('ACCOUNT', 'UPDATES', 'PROMOTIONS') NOT NULL DEFAULT 'ACCOUNT',
`password` varchar(191)  ,
`prefersLanguage` varchar(191) NOT NULL DEFAULT 'en-us',
`prefersColorScheme` ENUM('NO_PREFERENCE', 'LIGHT', 'DARK') NOT NULL DEFAULT 'NO_PREFERENCE',
`prefersReducedMotion` ENUM('NO_PREFERENCE', 'REDUCE') NOT NULL DEFAULT 'NO_PREFERENCE',
`prefersEmailId` int NOT NULL ,
`profilePictureUrl` varchar(191) NOT NULL DEFAULT 'https://unavatar.now.sh/fallback.png',
`role` ENUM('SUDO', 'USER') NOT NULL DEFAULT 'USER',
`timezone` varchar(191) NOT NULL DEFAULT 'America/Los_Angeles',
`twoFactorEnabled` boolean NOT NULL DEFAULT false,
`twoFactorSecret` varchar(191)  ,
`attributes` json  ,
`updatedAt` datetime(3) NOT NULL ,
PRIMARY KEY (`id`)
) DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci

CREATE TABLE `staart`.`groups` (
`autoJoinDomain` boolean NOT NULL DEFAULT false,
`createdAt` datetime NOT NULL DEFAULT CURRENT_TIMESTAMP,
`forceTwoFactor` boolean NOT NULL DEFAULT false,
`id` int NOT NULL  AUTO_INCREMENT,
`ipRestrictions` varchar(191)  ,
`name` varchar(191) NOT NULL ,
`onlyAllowDomain` boolean NOT NULL DEFAULT false,
`profilePictureUrl` varchar(191) NOT NULL DEFAULT 'https://unavatar.now.sh/fallback.png',
`attributes` json  ,
`updatedAt` datetime(3) NOT NULL ,
PRIMARY KEY (`id`)
) DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci

CREATE TABLE `staart`.`emails` (
`createdAt` datetime NOT NULL DEFAULT CURRENT_TIMESTAMP,
`email` varchar(191) NOT NULL ,
`id` int NOT NULL  AUTO_INCREMENT,
`isVerified` boolean NOT NULL DEFAULT false,
`updatedAt` datetime(3) NOT NULL ,
`userId` int NOT NULL ,
PRIMARY KEY (`id`)
) DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci

CREATE TABLE `staart`.`accessTokens` (
`createdAt` datetime NOT NULL DEFAULT CURRENT_TIMESTAMP,
`description` varchar(191)  ,
`expiresAt` datetime(3) NOT NULL ,
`id` int NOT NULL  AUTO_INCREMENT,
`accessToken` varchar(191) NOT NULL ,
`name` varchar(191)  ,
`scopes` json  ,
`updatedAt` datetime(3) NOT NULL ,
`userId` int NOT NULL ,
PRIMARY KEY (`id`)
) DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci

CREATE TABLE `staart`.`apiKeys` (
`createdAt` datetime NOT NULL DEFAULT CURRENT_TIMESTAMP,
`description` varchar(191)  ,
`expiresAt` datetime(3) NOT NULL ,
`id` int NOT NULL  AUTO_INCREMENT,
`ipRestrictions` json  ,
`apiKey` varchar(191) NOT NULL ,
`name` varchar(191)  ,
`groupId` int NOT NULL ,
`referrerRestrictions` varchar(191)  ,
`scopes` json  ,
`updatedAt` datetime(3) NOT NULL ,
PRIMARY KEY (`id`)
) DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci

CREATE TABLE `staart`.`approvedLocations` (
`createdAt` datetime NOT NULL DEFAULT CURRENT_TIMESTAMP,
`id` int NOT NULL  AUTO_INCREMENT,
`subnet` varchar(191) NOT NULL ,
`userId` int NOT NULL ,
PRIMARY KEY (`id`)
) DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci

CREATE TABLE `staart`.`backupCodes` (
`id` int NOT NULL  AUTO_INCREMENT,
`code` varchar(191) NOT NULL ,
`createdAt` datetime NOT NULL DEFAULT CURRENT_TIMESTAMP,
`updatedAt` datetime(3) NOT NULL ,
`isUsed` boolean NOT NULL DEFAULT false,
`userId` int NOT NULL ,
PRIMARY KEY (`id`)
) DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci

CREATE TABLE `staart`.`couponCodes` (
`id` int NOT NULL  AUTO_INCREMENT,
`code` varchar(191) NOT NULL ,
`createdAt` datetime NOT NULL DEFAULT CURRENT_TIMESTAMP,
`updatedAt` datetime(3) NOT NULL ,
`expiresAt` datetime(3)  ,
`maxUses` int NOT NULL DEFAULT 1000,
`usedCount` int NOT NULL DEFAULT 0,
`teamRestrictions` varchar(191)  ,
`amount` int NOT NULL ,
`currency` varchar(191) NOT NULL ,
`description` varchar(191)  ,
PRIMARY KEY (`id`)
) DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci

CREATE TABLE `staart`.`domains` (
`createdAt` datetime NOT NULL DEFAULT CURRENT_TIMESTAMP,
`domain` varchar(191) NOT NULL ,
`id` int NOT NULL  AUTO_INCREMENT,
`isVerified` boolean NOT NULL DEFAULT false,
`groupId` int NOT NULL ,
`updatedAt` datetime(3) NOT NULL ,
`verificationCode` varchar(191) NOT NULL ,
PRIMARY KEY (`id`)
) DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci

CREATE TABLE `staart`.`identities` (
`createdAt` datetime NOT NULL DEFAULT CURRENT_TIMESTAMP,
`id` int NOT NULL  AUTO_INCREMENT,
`loginName` varchar(191) NOT NULL ,
`type` ENUM('GOOGLE', 'APPLE', 'SLACK') NOT NULL ,
`updatedAt` datetime(3) NOT NULL ,
`userId` int NOT NULL ,
PRIMARY KEY (`id`)
) DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci

CREATE TABLE `staart`.`memberships` (
`createdAt` datetime NOT NULL DEFAULT CURRENT_TIMESTAMP,
`id` int NOT NULL  AUTO_INCREMENT,
`groupId` int NOT NULL ,
`role` ENUM('OWNER', 'ADMIN', 'MEMBER') NOT NULL DEFAULT 'MEMBER',
`updatedAt` datetime(3) NOT NULL ,
`userId` int NOT NULL ,
PRIMARY KEY (`id`)
) DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci

CREATE TABLE `staart`.`sessions` (
`createdAt` datetime NOT NULL DEFAULT CURRENT_TIMESTAMP,
`id` int NOT NULL  AUTO_INCREMENT,
`ipAddress` varchar(191) NOT NULL ,
`token` varchar(191) NOT NULL ,
`updatedAt` datetime(3) NOT NULL ,
`userAgent` varchar(191) NOT NULL ,
`city` varchar(191)  ,
`region` varchar(191)  ,
`timezone` varchar(191)  ,
`countryCode` varchar(191)  ,
`browser` varchar(191)  ,
`operatingSystem` varchar(191)  ,
`userId` int NOT NULL ,
PRIMARY KEY (`id`)
) DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci

CREATE TABLE `staart`.`webhooks` (
`contentType` varchar(191) NOT NULL DEFAULT 'application/json',
`createdAt` datetime NOT NULL DEFAULT CURRENT_TIMESTAMP,
`event` varchar(191) NOT NULL ,
`id` int NOT NULL  AUTO_INCREMENT,
`isActive` boolean NOT NULL DEFAULT false,
`lastFiredAt` datetime(3)  ,
`groupId` int NOT NULL ,
`secret` varchar(191)  ,
`updatedAt` datetime(3) NOT NULL ,
`url` varchar(191) NOT NULL ,
PRIMARY KEY (`id`)
) DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci

CREATE  INDEX `userId` ON `staart`.`emails`(`userId`)

CREATE  INDEX `userId` ON `staart`.`accessTokens`(`userId`)

CREATE  INDEX `userId` ON `staart`.`backupCodes`(`userId`)

CREATE  INDEX `groupId` ON `staart`.`domains`(`groupId`)

CREATE  INDEX `userId` ON `staart`.`identities`(`userId`)

CREATE  INDEX `groupId` ON `staart`.`memberships`(`groupId`)

CREATE  INDEX `userId` ON `staart`.`memberships`(`userId`)

CREATE  INDEX `userId` ON `staart`.`sessions`(`userId`)

CREATE  INDEX `groupId` ON `staart`.`webhooks`(`groupId`)

ALTER TABLE `staart`.`users` ADD FOREIGN KEY (`prefersEmailId`) REFERENCES `staart`.`emails`(`id`) ON DELETE CASCADE ON UPDATE CASCADE

ALTER TABLE `staart`.`emails` ADD FOREIGN KEY (`userId`) REFERENCES `staart`.`users`(`id`) ON DELETE CASCADE ON UPDATE CASCADE

ALTER TABLE `staart`.`accessTokens` ADD FOREIGN KEY (`userId`) REFERENCES `staart`.`users`(`id`) ON DELETE CASCADE ON UPDATE CASCADE

ALTER TABLE `staart`.`apiKeys` ADD FOREIGN KEY (`groupId`) REFERENCES `staart`.`groups`(`id`) ON DELETE CASCADE ON UPDATE CASCADE

ALTER TABLE `staart`.`approvedLocations` ADD FOREIGN KEY (`userId`) REFERENCES `staart`.`users`(`id`) ON DELETE CASCADE ON UPDATE CASCADE

ALTER TABLE `staart`.`backupCodes` ADD FOREIGN KEY (`userId`) REFERENCES `staart`.`users`(`id`) ON DELETE CASCADE ON UPDATE CASCADE

ALTER TABLE `staart`.`domains` ADD FOREIGN KEY (`groupId`) REFERENCES `staart`.`groups`(`id`) ON DELETE CASCADE ON UPDATE CASCADE

ALTER TABLE `staart`.`identities` ADD FOREIGN KEY (`userId`) REFERENCES `staart`.`users`(`id`) ON DELETE CASCADE ON UPDATE CASCADE

ALTER TABLE `staart`.`memberships` ADD FOREIGN KEY (`groupId`) REFERENCES `staart`.`groups`(`id`) ON DELETE CASCADE ON UPDATE CASCADE

ALTER TABLE `staart`.`memberships` ADD FOREIGN KEY (`userId`) REFERENCES `staart`.`users`(`id`) ON DELETE CASCADE ON UPDATE CASCADE

ALTER TABLE `staart`.`sessions` ADD FOREIGN KEY (`userId`) REFERENCES `staart`.`users`(`id`) ON DELETE CASCADE ON UPDATE CASCADE

ALTER TABLE `staart`.`webhooks` ADD FOREIGN KEY (`groupId`) REFERENCES `staart`.`groups`(`id`) ON DELETE CASCADE ON UPDATE CASCADE
```

## Changes

```diff
diff --git schema.prisma schema.prisma
migration ..20200803235103
--- datamodel.dml
+++ datamodel.dml
@@ -1,0 +1,247 @@
+generator client {
+  provider = "prisma-client-js"
+}
+
+datasource mysql {
+  provider = "mysql"
+  url = "***"
+}
+
+enum Gender {
+  MALE
+  FEMALE
+  NONBINARY
+  UNKNOWN
+}
+
+enum NotificationEmails {
+  ACCOUNT
+  UPDATES
+  PROMOTIONS
+}
+
+enum PrefersColorScheme {
+  NO_PREFERENCE
+  LIGHT
+  DARK
+}
+
+enum PrefersReducedMotion {
+  NO_PREFERENCE
+  REDUCE
+}
+
+enum UserRole {
+  SUDO
+  USER
+}
+
+enum MembershipRole {
+  OWNER
+  ADMIN
+  MEMBER
+}
+
+enum IdentityType {
+  GOOGLE
+  APPLE
+  SLACK
+}
+
+model users {
+  checkLocationOnLogin Boolean              @default(false)
+  countryCode          String               @default("us")
+  createdAt            DateTime             @default(now())
+  gender               Gender               @default(UNKNOWN)
+  id                   Int                  @default(autoincrement()) @id
+  name                 String
+  notificationEmails   NotificationEmails   @default(ACCOUNT)
+  password             String?
+  prefersLanguage      String               @default("en-us")
+  prefersColorScheme   PrefersColorScheme   @default(NO_PREFERENCE)
+  prefersReducedMotion PrefersReducedMotion @default(NO_PREFERENCE)
+  prefersEmail         emails               @relation("userPrefersEmail", fields: [prefersEmailId], references: [id])
+  prefersEmailId       Int
+  profilePictureUrl    String               @default("https://unavatar.now.sh/fallback.png")
+  role                 UserRole             @default(USER)
+  timezone             String               @default("America/Los_Angeles")
+  twoFactorEnabled     Boolean              @default(false)
+  twoFactorSecret      String?
+  attributes           Json?
+  updatedAt            DateTime             @updatedAt
+  emails               emails[]             @relation("userEmails")
+  accessTokens         accessTokens[]       @relation("userAccessTokens")
+  approvedLocations    approvedLocations[]  @relation("userApprovedLocations")
+  backupCodes          backupCodes[]        @relation("userBackupCodes")
+  identities           identities[]         @relation("userIdentities")
+  memberships          memberships[]        @relation("userMemberships")
+  sessions             sessions[]           @relation("userSessions")
+}
+
+model groups {
+  autoJoinDomain    Boolean       @default(false)
+  createdAt         DateTime      @default(now())
+  forceTwoFactor    Boolean       @default(false)
+  id                Int           @default(autoincrement()) @id
+  ipRestrictions    String?
+  name              String
+  onlyAllowDomain   Boolean       @default(false)
+  profilePictureUrl String        @default("https://unavatar.now.sh/fallback.png")
+  attributes        Json?
+  updatedAt         DateTime      @updatedAt
+  apiKeys           apiKeys[]     @relation("groupApiKeys")
+  domains           domains[]     @relation("groupDomains")
+  memberships       memberships[] @relation("groupMemberships")
+  webhooks          webhooks[]    @relation("groupWebhooks")
+}
+
+model emails {
+  createdAt  DateTime @default(now())
+  email      String
+  id         Int      @default(autoincrement()) @id
+  isVerified Boolean  @default(false)
+  updatedAt  DateTime @updatedAt
+  user       users    @relation("userEmails", fields: [userId], references: [id])
+  userId     Int
+
+  @@index([userId], name: "userId")
+  users users[] @relation("userPrefersEmail")
+}
+
+model accessTokens {
+  createdAt   DateTime @default(now())
+  description String?
+  expiresAt   DateTime
+  id          Int      @default(autoincrement()) @id
+  accessToken String
+  name        String?
+  scopes      Json?
+  updatedAt   DateTime @updatedAt
+  user        users    @relation("userAccessTokens", fields: [userId], references: [id])
+  userId      Int
+
+  @@index([userId], name: "userId")
+}
+
+model apiKeys {
+  createdAt            DateTime @default(now())
+  description          String?
+  expiresAt            DateTime
+  id                   Int      @default(autoincrement()) @id
+  ipRestrictions       Json?
+  apiKey               String
+  name                 String?
+  group                groups   @relation("groupApiKeys", fields: [groupId], references: [id])
+  groupId              Int
+  referrerRestrictions String?
+  scopes               Json?
+  updatedAt            DateTime @updatedAt
+}
+
+model approvedLocations {
+  createdAt DateTime @default(now())
+  id        Int      @default(autoincrement()) @id
+  subnet    String
+  user      users    @relation("userApprovedLocations", fields: [userId], references: [id])
+  userId    Int
+}
+
+model backupCodes {
+  id        Int      @default(autoincrement()) @id
+  code      String
+  createdAt DateTime @default(now())
+  updatedAt DateTime @updatedAt
+  isUsed    Boolean  @default(false)
+  user      users    @relation("userBackupCodes", fields: [userId], references: [id])
+  userId    Int
+
+  @@index([userId], name: "userId")
+}
+
+model couponCodes {
+  id               Int       @default(autoincrement()) @id
+  code             String
+  createdAt        DateTime  @default(now())
+  updatedAt        DateTime  @updatedAt
+  expiresAt        DateTime?
+  maxUses          Int       @default(1000)
+  usedCount        Int       @default(0)
+  teamRestrictions String?
+  amount           Int
+  currency         String
+  description      String?
+}
+
+model domains {
+  createdAt        DateTime @default(now())
+  domain           String
+  id               Int      @default(autoincrement()) @id
+  isVerified       Boolean  @default(false)
+  group            groups   @relation("groupDomains", fields: [groupId], references: [id])
+  groupId          Int
+  updatedAt        DateTime @updatedAt
+  verificationCode String
+
+  @@index([groupId], name: "groupId")
+}
+
+model identities {
+  createdAt DateTime     @default(now())
+  id        Int          @default(autoincrement()) @id
+  loginName String
+  type      IdentityType
+  updatedAt DateTime     @updatedAt
+  user      users        @relation("userIdentities", fields: [userId], references: [id])
+  userId    Int
+
+  @@index([userId], name: "userId")
+}
+
+model memberships {
+  createdAt DateTime       @default(now())
+  id        Int            @default(autoincrement()) @id
+  group     groups         @relation("groupMemberships", fields: [groupId], references: [id])
+  groupId   Int
+  role      MembershipRole @default(MEMBER)
+  updatedAt DateTime       @updatedAt
+  user      users          @relation("userMemberships", fields: [userId], references: [id])
+  userId    Int
+
+  @@index([groupId], name: "groupId")
+  @@index([userId], name: "userId")
+}
+
+model sessions {
+  createdAt       DateTime @default(now())
+  id              Int      @default(autoincrement()) @id
+  ipAddress       String
+  token           String
+  updatedAt       DateTime @updatedAt
+  userAgent       String
+  city            String?
+  region          String?
+  timezone        String?
+  countryCode     String?
+  browser         String?
+  operatingSystem String?
+  user            users    @relation("userSessions", fields: [userId], references: [id])
+  userId          Int
+
+  @@index([userId], name: "userId")
+}
+
+model webhooks {
+  contentType String    @default("application/json")
+  createdAt   DateTime  @default(now())
+  event       String
+  id          Int       @default(autoincrement()) @id
+  isActive    Boolean   @default(false)
+  lastFiredAt DateTime?
+  group       groups    @relation("groupWebhooks", fields: [groupId], references: [id])
+  groupId     Int
+  secret      String?
+  updatedAt   DateTime  @updatedAt
+  url         String
+
+  @@index([groupId], name: "groupId")
+}
```


