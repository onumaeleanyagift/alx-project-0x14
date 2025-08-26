# alx-project-0x14

This project explores The Movie Database (TMDB) API, a comprehensive web service for movie and TV show data.

## API Overview

The Movie Database (TMDB) API is a comprehensive RESTful web service that provides access to extensive movie, TV show, and actor data. This is version 3 of The Movie Database (TMDB) API, which contains the definitive list of currently available methods for movie, tv, actor and image API. The API offers rich metadata including plot summaries, cast and crew information, release dates, ratings, images, and much more. MoviesDatabase provides complete and updated data for over 9 million titles (movies, series and episodes) and 11 million actors / crew and cast members. It serves as an invaluable resource for developers building entertainment-focused applications, offering both basic information retrieval and advanced discovery features.

## Version

The current version of The Movie Database API is **Version 3**. This version provides stable and well-documented endpoints with comprehensive coverage of movie and TV show data.

## Available Endpoints

The TMDB API offers several categories of endpoints:

**Movie Endpoints:**
- GET /movie/{movie_id} - Retrieve detailed information about a specific movie
- GET /movie/{movie_id}/credits - Get cast and crew information for a movie
- GET /movie/popular - Get a list of currently popular movies
- GET /movie/top_rated - Fetch top-rated movies
- GET /movie/upcoming - Get upcoming movie releases
- GET /movie/now_playing - Retrieve movies currently in theaters

**Search Endpoints:**
- GET /search/movie - Search for movies by title or keywords
- GET /search/tv - Search for TV shows
- GET /search/person - Search for actors, directors, and other crew members

**Discovery Endpoints:**
- GET /discover/movie - Discover movies based on filters like genre, year, rating
- GET /discover/tv - Discover TV shows with various filtering options

**TV Show Endpoints:**
- GET /tv/{tv_id} - Get detailed TV show information
- GET /tv/{tv_id}/credits - Retrieve cast and crew for TV shows
- GET /tv/popular - Get popular TV shows

**Person Endpoints:**
- GET /person/{person_id} - Get detailed information about actors and crew members
- GET /person/{person_id}/movie_credits - Get movie credits for a specific person

**Configuration Endpoints:**
- GET /configuration - Get API configuration including image base URLs
- GET /genre/movie/list - Retrieve list of movie genres
- GET /genre/tv/list - Get list of TV show genres

## Request and Response Format

All API requests follow this base URL pattern:
```
https://api.themoviedb.org/3/{endpoint}?api_key={your_api_key}&{additional_parameters}
```

**Example Request:**
```
GET https://api.themoviedb.org/3/movie/550?api_key=YOUR_API_KEY&language=en-US
```

**Example Response for Movie Details:**
```json
{
  "adult": false,
  "backdrop_path": "/fCayJrkfRaCRCTh8GqN30f8oyQF.jpg",
  "belongs_to_collection": null,
  "budget": 63000000,
  "genres": [
    {
      "id": 18,
      "name": "Drama"
    }
  ],
  "homepage": "",
  "id": 550,
  "imdb_id": "tt0137523",
  "original_language": "en",
  "original_title": "Fight Club",
  "overview": "A ticking-time-bomb insomniac...",
  "popularity": 61.416,
  "poster_path": "/pB8BM7pdSp6B6Ih7QZ4DrQ3PmJK.jpg",
  "production_companies": [...],
  "release_date": "1999-10-15",
  "revenue": 100853753,
  "runtime": 139,
  "status": "Released",
  "tagline": "Mischief. Mayhem. Soap.",
  "title": "Fight Club",
  "vote_average": 8.433,
  "vote_count": 26280
}
```

Common response fields include:
- id: Unique identifier for the resource
- title/name: Title of the movie or name of TV show/person
- overview/biography: Descriptive text
- poster_path/profile_path: Relative path to image
- vote_average: User rating (1-10 scale)
- popularity: Popularity score
- release_date/first_air_date: Release information

## Authentication

You can request an API key by logging in to your account on TMDB and clicking the API section. The default method to authenticate is with your access token.

**Authentication Methods:**

1. Query Parameter (Recommended):
   ```
   GET https://api.themoviedb.org/3/movie/popular?api_key=YOUR_API_KEY
   ```

2. Authorization Header:
   ```
   Authorization: Bearer YOUR_ACCESS_TOKEN
   ```

**Getting Your API Key:**
1. Create a free account at themoviedb.org
2. Go to your account settings
3. Click on the "API" section
4. Request an API key for developer use
5. Agree to the terms of use to receive your key

## Error Handling

The API uses standard HTTP status codes and returns detailed error information:

**Common Status Codes:**
- 200: Success
- 401: Invalid API key or unauthorized access
- 404: Resource not found
- 422: Request couldn't be parsed
- 500: Internal server error

**Error Response Format:**
```json
{
  "status_code": 7,
  "status_message": "Invalid API key: You must be granted a valid key.",
  "success": false
}
```

**Error Handling Best Practices:**
- Always check the HTTP status code before processing the response
- Parse error messages from the JSON response for user-friendly feedback
- Implement retry logic for temporary failures (5xx errors)
- Cache successful responses to reduce API calls
- Handle rate limiting gracefully by implementing exponential backoff

**Common Error Scenarios:**
- Invalid API Key: Check your API key is correctly formatted and active
- Resource Not Found: Verify the ID exists and is publicly available
- Rate Limited: Implement request throttling and retry after specified time

## Usage Limits and Best Practices

**Rate Limits:**
The API currently rate limits requests to 30 requests every 10 seconds. This limit is enforced per IP address.

**Best Practices:**

*Request Optimization:*
- Cache responses locally to minimize API calls
- Use appropriate page sizes for paginated endpoints
- Batch requests when possible rather than making individual calls
- Implement request queuing to respect rate limits

*Data Management:*
- Store frequently accessed data locally with appropriate refresh intervals
- Use configuration endpoints to get image base URLs and other constants
- Implement proper image loading using the configuration data
- Handle pagination properly for large result sets

*Performance Tips:*
- Request only needed data by using appropriate endpoints
- Use language parameters to get localized content when available
- Implement proper error handling and fallback mechanisms
- Monitor your usage to stay within rate limits

*Respectful Usage:*
- Don't hammer the API with unnecessary requests
- Cache images and data appropriately to reduce server load
- Use appropriate user agents to identify your application
- Follow the terms of service and attribution requirements

**Usage Monitoring:**
- Monitor your request patterns to identify optimization opportunities
- Implement logging to track API usage and errors
- Set up alerts for when approaching rate limits
- Consider implementing circuit breakers for resilient applications

---

For more detailed information, visit the official TMDB API Documentation at https://developer.themoviedb.org/docs/getting-started