<script lang="ts">
    import './page.css';

    import logo from '$lib/assets/msu(1).png';
    import {Calendar, TimeGrid} from '@event-calendar/core';
    import events from "$lib/assets/events.json";
 
    let options = $state({
        view: 'timeGridWeek',
        events: events,
        //times are in World time
        slotMinTime: '15:00:00', 
        slotMaxTime: '22:00:00', 
        eventDidMount: (info) => {
            // Add native browser tooltip on hover
            const props = info.event.extendedProps;
            if (props && props.description) {
                info.el.title = `${info.event.title}\n\n${props.description}\n\nlocation: ${props.location}\ntime: ${props.time}`;
            }
        }
    });
</script>

<div class="page">
	<!-- Hero Section -->
	<section class="hero">
		<div class="hero-content">
			<img src={logo} alt="MSU Logo" class="hero-logo" />
            <h1>Welcome to MSU Game Design Club</h1>

			<p>A club focused on building, collaberation, and celebration of game design</p>
			<a href="#about" class="cta-button">Learn More</a>
		</div>
	</section>

	<!-- Main Content -->
	<div class="container">
		<!-- About Section -->
		<section id="about" class="section">
			<h2 class="section-title">About Us</h2>
			<div class="about-content">
				<p>The Game Design Club at Morehead State University aims to creates a safe, open space for students from all backgrounds to discuss and participate in game design and development. Whether you're interested in programming, art, storytelling, or sound design, our club encourages .</p>

			</div>
        </section>

		<!-- Activities Section -->
		<section id="activities" class="section">
			<h2 class="section-title">Activities & Events</h2>
			<div class="activities-grid">
				<div class="activity-card">
					<div class="activity-icon"></div>
                    <h3 text-align="">Game Jams</h3>
                    <p> Build teams to build games around themes/prompts for prizes.
                    </p>
				</div>
				<div class="activity-card">
					<div class="activity-icon"></div>
                    <h3>Presentations</h3>

					<p>Student and officer led presentations exploring topics in game design, storytelling, programming, artistic design, and more.</p>
				</div>
				<div class="activity-card">
					<div class="activity-icon"></div>
					<h3>Debug Days</h3>
					<p>Bring your ongoing projects and receive constructive feedback and advice on design and technical aspects in a supportive setting.</p>
				</div>
				<div class="activity-card">
					<div class="activity-icon"></div>
                    <h3>Workshops</h3>
                    <p>Activities centered around building hands on experience with tools based in game design</p>
				</div>
			</div>
		</section>

		<!-- Calendar Section -->
		<section id="events" class="section">
			<h2 class="section-title">Upcoming Events</h2>
			<Calendar plugins={[TimeGrid]} {options} />
		</section>
	</div>
</div>

