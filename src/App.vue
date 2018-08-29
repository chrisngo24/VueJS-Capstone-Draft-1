<!-- PARENT COMPONENT -->
<template>
  <div id="app">
     <!-- navbar-->
    <header class="header">
      <nav class="navbar navbar-expand-lg">
        <div class="container"><a href="/#/" class="navbar-brand"><img src="https://d19m59y37dris4.cloudfront.net/jobs/2-0-1/img/logo.png" alt="logo" class="d-none d-lg-block"><img src="https://d19m59y37dris4.cloudfront.net/jobs/2-0-1/img/logo-small.png" alt="logo" class="d-block d-lg-none"><span class="sr-only">Go to homepage</span></a>
          <!-- <button type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation" class="navbar-toggler navbar-toggler-right">Menu<i class="fa fa-bars"></i></button> -->

          <div id="navbarSupportedContent" class="collapse navbar-collapse">
            <ul class="navbar-nav ml-auto">
              <li class="nav-item active"><a href="/#/" class="nav-link">Home <span class="sr-only">(current)</span></a></li>
              <li class="nav-item"><a href="/#/about" class="nav-link">About Us</a></li>
              <li class="nav-item dropdown"><a id="community" href="/#/signup" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false" class="nav-link dropdown-toggle">Conveyers</a>
                <div aria-labelledby="community" class="dropdown-menu"><a href="/#/login" class="dropdown-item">Login</a><a href="/#/signup" class="dropdown-item">Signup</a><!-- <a href="client-applicants.html" class="dropdown-item">Applicants                </a><a href="client-job.html" class="dropdown-item">Post a new job  </a> --></div>
              </li>

             <!--  <li class="nav-item dropdown"><a id="pages" href="#" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false" class="nav-link dropdown-toggle">Pages</a>
                <div aria-labelledby="pages" class="dropdown-menu"><a href="index.html" class="dropdown-item">Home</a><a href="category.html" class="dropdown-item">Job Listing</a><a href="detail.html" class="dropdown-item">Job Detail                </a><a href="about.html" class="dropdown-item">About                </a><a href="contact.html" class="dropdown-item">Contact                </a><a href="blog.html" class="dropdown-item">Blog Listing                </a><a href="post.html" class="dropdown-item">Blog Post                </a><a href="packages.html" class="dropdown-item">Pricing packages    </a><a href="testimonials.html" class="dropdown-item">Testimonials    </a><a href="text.html" class="dropdown-item">Text Page    </a><a href="faq.html" class="dropdown-item">FAQ</a></div>
              </li> -->
              <li class="nav-item dropdown"><a href="#loginModal" data-toggle="modal" class="btn navbar-btn btn-outline-light mb-5 mb-lg-0"> <i class="fa fa-sign-in"></i>Login</a></li>
            </ul>
          </div>
        </div>
      </nav>
    </header>

    <!--   <div>
        <h1 class="title">Navstone</h1>
      </div>
      <div class="btn-toolbar" role="toolbar" aria-label="Toolbar with button groups">
        <div class="btn-group mr-2" role="group" aria-label="First group">
          <button type="button" class="btn-nav"><a href="/#/">Home</a></button>
          <button type="button" class="btn-nav"><a href="/#/about">About</a></button>
          <button type="button" class="btn-nav">Account</button>
          <button type="button" class="btn-nav"><a href="/#/signup">Signup</a></button>
          <button type="button" class="btn-nav"><a href="/#/login">Login</a></button>
          <button type="button" class="btn-nav"><a href="/#/logout">Logout</a></button>
        </div>
      </div> -->

    <router-view/>

    <footer class="footer">
      <div class="footer__block">
        <div class="container">
          <div class="row">
            <div class="col-lg-4 col-md-12 mb-5">
              <h4 class="h5">About Jobs</h4>
              <p>Jobs is a <strong>Bootstrap 3 jobs board theme </strong> developed in the middle of Europe by <a href="http://ondrejsvestka.cz/">Ondrej Svestka</a></p>
              <p> Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vivamus magna. Cras in mi at felis aliquet congue. </p>
            </div>
            <div class="col-lg-4 col-md-6 mb-5">
              <h4 class="h5">This Theme</h4>
              <ul class="list-unstyled">
                <li><a href="index.html">Home</a></li>
                <li><a href="category.html">Jobs Listing</a></li>
                <li><a href="detail.html">Job detail</a></li>
                <li><a href="about.html">About</a></li>
                <li><a href="contact.html">Contact</a></li>
                <li><a href="blog.html">Blog listing</a></li>
                <li><a href="post.html">Blog Post</a></li>
                <li><a href="packages.html">Pricing packages</a></li>
                <li><a href="testimonials.html">Testimonials</a></li>
                <li><a href="text.html">Text page</a></li>
                <li><a href="faq.html">FAQ</a></li>
              </ul>
            </div>
            <div class="col-lg-4 col-md-6">
              <h4 class="h5">Our offices</h4>
              <h5>London</h5>
              <p> Donec eleifend<br />libero at sagittis<br />mollis + 44 2556 789 8799</p>
              <h5>Paris</h5>
              <p> Donec eleifend<br />libero at sagittis<br />mollis + 41 2556 789 8799</p>
            </div>
          </div>
          <div class="row">
            <div class="col-lg-4 col-md-6 mb-5">
              <h4 class="h5">Client zone</h4>
              <ul class="list-unstyled">
                <li><a href="client-register.html">Login or Register</a></li>
                <li><a href="client-dashboard.html">Dashboard</a></li>
                <li><a href="client-applicants.html">Applicants</a></li>
                <li><a href="client-job.html">Post a new job</a></li>
              </ul>
            </div>
            <div class="col-lg-4 col-md-6 mb-5">
              <h4 class="h5">Let's be Friends</h4>
              <p class="social"><a href="#" data-animate-hover="pulse" class="external facebook"><i class="fa fa-facebook"></i></a><a href="#" data-animate-hover="pulse" class="external gplus"><i class="fa fa-google-plus"></i></a><a href="#" data-animate-hover="pulse" class="external twitter"><i class="fa fa-twitter"></i></a><a href="#" data-animate-hover="pulse" class="email"><i class="fa fa-envelope"></i></a></p>
            </div>
            <div class="col-lg-4 col-md-12 mb-5">
              <h4 class="h5">News and Updates</h4>
              <p>Sign up to get weekly portion of fresh jobs and news from us.</p>
              <form class="footer__newsletter">
                <div class="input-group">
                  <input type="text" placeholder="Enter your email address" aria-describedby="emailAddress" class="form-control">
                  <div class="input-group-append">
                    <button id="emailAddress" type="button" class="btn btn-default input-group-text"><i class="fa fa-send"></i></button>
                  </div>
                </div>
              </form>
            </div>
          </div>
        </div>
      </div>
      <div class="footer__copyright">
        <div class="container">
          <div class="row">
            <div class="col-md-6 text-md-left text-center">
              <p>&copy;2017 Best company</p>
            </div>
            <div class="col-md-6 text-md-right text-center">
              <p class="credit">Theme by <a href="https://ondrejsvestka.cz/">Ondrej Svestka</a></p>
            </div>
          </div>
        </div>
      </div>
    </footer>
  </div>
</template>

<style>

</style>
