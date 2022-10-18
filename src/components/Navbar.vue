<template>
  <nav class="navbar navbar-expand-lg navbar-light bg-light">
    <RouterLink class="navbar-brand" to="/">Beauty Life</RouterLink>
    <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarSupportedContent">
      <ul class="navbar-nav mr-auto">
        <li class="nav-item active">
          <RouterLink class="nav-link" to="/">Home
            <span class="sr-only">(current)</span>
          </RouterLink>
        </li>
        <li class="nav-item">
          <RouterLink class="nav-link" to="/favorite">favorite</RouterLink>
        </li>
      </ul>
    </div>
  </nav>
</template>

<style scoped>
nav{
  width: 100%;
  background: url('https://images.pexels.com/photos/7256145/pexels-photo-7256145.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=2') no-repeat center center;
  background-size: cover;
}
nav .navbar-brand{
  font-weight: 700;
  color: rgb(238, 24, 59);
}
nav .navbar-brand:hover{
  color: rgb(49, 45, 46);
}
nav .navbar-collapse .navbar-nav .nav-item .nav-link{
  color: rgb(238, 24, 59);
}
nav .navbar-collapse .navbar-nav .nav-item .nav-link:hover{
  color: rgb(49, 45, 46);
}
</style>