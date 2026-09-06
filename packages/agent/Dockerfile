# Builds the palserver agent (with the web UI bundled) into a single image.
FROM node:22-alpine AS build
# 局域网代理(构建期下载依赖用;运行期 node 不读这俩变量,不加在 runtime 阶段)
ENV HTTP_PROXY=http://192.168.1.109:7890
ENV HTTPS_PROXY=http://192.168.1.109:7890
RUN corepack enable
WORKDIR /app
ENV CI=true
COPY . .
RUN pnpm install --frozen-lockfile && pnpm -r build

FROM node:22-alpine
RUN corepack enable
WORKDIR /app
COPY --from=build /app/package.json /app/pnpm-workspace.yaml /app/pnpm-lock.yaml ./
COPY --from=build /app/packages/shared/package.json packages/shared/
COPY --from=build /app/packages/shared/dist packages/shared/dist
COPY --from=build /app/packages/agent/package.json packages/agent/
COPY --from=build /app/packages/agent/dist packages/agent/dist
COPY --from=build /app/packages/web/dist packages/web/dist
# 遊戲容器映像的 build context(palserver/vanilla、palserver/wine)——
# agent 首次啟動實例時會現場 docker build,缺了會報「找不到 build context」
COPY --from=build /app/images images
RUN pnpm install --frozen-lockfile --prod --filter @palserver/agent --filter @palserver/shared
EXPOSE 8250
CMD ["node", "packages/agent/dist/index.js"]
