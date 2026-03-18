<template>
  <main>
    <div class="login-container">
      <div class="login-main">
        <div class="login-main__content">
          <div class="login-brand mb-5">
            <login-company-logo class="login-brand__logo" :aria-label="altLogo" />
          </div>
          <h1 v-if="customizableGuiName" class="h3 mb-5">
            {{ customizableGuiName }}
          </h1>
          <router-view class="login-form form-background" />
        </div>
      </div>
      <div class="login-aside">
        <div class="login-aside__logo-brand">
          <!-- Add Secondary brand logo if needed -->
        </div>
        <div class="login-aside__logo-bmc">
          <datenbmc-logo class="login-aside__logo" aria-label="DatenBMC" />
        </div>
      </div>
    </div>
  </main>
</template>

<script>
import DatenbmcLogo from '@/assets/images/datenbmc-logo.svg?component';

export default {
  name: 'LoginLayout',
  components: {
    LoginCompanyLogo: DatenbmcLogo,
    DatenbmcLogo,
  },
  data() {
    return {
      altLogo: import.meta.env.VITE_COMPANY_NAME || 'DatenBMC',
      customizableGuiName: import.meta.env.VITE_GUI_NAME || '',
    };
  },
};
</script>

<style lang="scss" scoped>
.login-container {
  background: $gray-100;
  display: flex;
  flex-direction: column;
  gap: $spacer * 2;
  max-width: 1400px;
  min-width: 320px;
  min-height: 100vh;
  justify-content: space-around;

  @include media-breakpoint-up('md') {
    background: $white;
    flex-direction: row;
  }
}

.login-main {
  min-height: 50vh;
  padding: $spacer * 3;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;

  @include media-breakpoint-up('md') {
    background: $gray-100;
    flex: 1 1 75%;
    min-height: 100vh;
  }
}

.login-main__content {
  width: min(100%, 420px);
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: $spacer * 1.5;
  position: relative;
  z-index: 1;
}

.login-brand {
  width: 100%;
  max-width: 320px;
  margin-bottom: 0 !important;
  flex: 0 0 auto;
}

.login-brand__logo {
  display: block;
  width: 100%;
  height: auto;
}

:deep(.login-brand__logo svg) {
  display: block;
  width: 100%;
  height: auto;
  max-width: 100%;
}

// Reach into the route component root element
:deep(.login-form) {
  width: 100%;

  @include media-breakpoint-up('md') {
    max-width: 360px;
  }
}

.login-aside {
  display: flex;
  align-items: flex-end;
  justify-content: flex-end;
  gap: $spacer * 1.5;
  margin-inline-end: $spacer * 3;
  margin-bottom: $spacer;

  @include media-breakpoint-up('md') {
    min-height: 100vh;
    padding-bottom: $spacer;
    flex: 1 1 25%;
    margin-bottom: 0;
  }
}

.login-aside__logo-brand:not(:empty) {
  &::after {
    content: '';
    display: inline-block;
    height: 2.5rem;
    width: 2px;
    background-color: $gray-200;
    margin-inline-start: $spacer * 1.5;
    vertical-align: middle;
  }
}

.login-aside__logo-bmc {
  width: 100%;
  max-width: 260px;
  flex: 0 0 auto;
}

.login-aside__logo {
  display: block;
  width: 100%;
  height: auto;
}

:deep(.login-aside__logo svg) {
  display: block;
  width: 100%;
  height: auto;
  max-width: 100%;
}
</style>
