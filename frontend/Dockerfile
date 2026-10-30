FROM node:22-alpine AS builder

# Working directory

WORKDIR /app

#Get all code in

COPY . .

# Install dependenices (stores to /node_modeules

RUN npm install --legacy-peer-deps

#Frontend Build (stores to /dist)

RUN npm run build

# ---------- Stage 1 ends --------
# ---------- Stage 2 starts ------

FROM dhi.io/node:26 AS runner

#Working directory

WORKDIR /app

COPY --from=builder /app/dist ./dist
COPY --from=builder /app/node_modules ./node_modules

COPY vite.preview.config.js ./vite.config.js

# Run the app

CMD ["node","./node_modules/.bin/vite","preview","--host", "0.0.0.0","--port","4173"]

