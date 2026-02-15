# Requirements Document: SchemeSahayak

## Introduction

SchemeSahayak is a pan-India browser-based, voice-first AI assistant designed to help citizens—especially those in rural areas or with low literacy—discover and access government schemes. The system uses voice and text input in multiple Indian languages, leverages Amazon Bedrock for intelligent eligibility matching across 30+ central schemes and state-specific programs, and provides simple, accessible guidance through progressive clarifying questions.

## Glossary

- **SchemeSahayak**: The AI assistant system for government scheme discovery
- **User**: A citizen seeking information about government schemes
- **Scheme**: A government program offering benefits or services
- **Eligibility_Matcher**: The component that determines which schemes a user qualifies for
- **Voice_Interface**: The component handling speech-to-text and text-to-speech
- **Session**: A single interaction period with the system
- **Bedrock_Service**: Amazon Bedrock AI service for dynamic matching and reasoning
- **Query_Processor**: The component that interprets user input and extracts relevant information
- **Clarification_Engine**: The component that generates progressive yes/no questions
- **State_Context**: The user's selected or detected state/region
- **Low_Bandwidth_Mode**: Optimized mode for slow internet connections
- **Summary**: A shareable document of matched schemes and next steps

## Requirements

### Requirement 1: Multi-Language Voice and Text Input

**User Story:** As a citizen with low literacy or limited typing ability, I want to speak or type my query in my preferred language, so that I can access scheme information without language barriers.

#### Acceptance Criteria

1. WHEN a user speaks in Hindi, English, or a regional language, THE Voice_Interface SHALL convert the speech to text with the detected language
2. WHEN a user types input in Hindi, English, or a regional language, THE Query_Processor SHALL accept and process the text input
3. WHEN the Voice_Interface receives audio input, THE System SHALL process it within 3 seconds for low-latency interaction
4. WHEN a user provides input like "Main Maharashtra ka kisaan hoon", THE Query_Processor SHALL extract relevant context (state: Maharashtra, occupation: farmer)
5. WHEN a user provides a general query without specific details, THE System SHALL accept the input and proceed to clarification

### Requirement 2: State Selection and Detection

**User Story:** As a user, I want the system to know my state context, so that I receive relevant state-specific scheme information.

#### Acceptance Criteria

1. WHEN a user first accesses the system, THE System SHALL present an option to select their state
2. WHEN a user mentions their state in voice or text input, THE Query_Processor SHALL extract and set the State_Context automatically
3. WHEN State_Context is set, THE System SHALL persist it for the duration of the session
4. WHEN a user changes their state selection, THE System SHALL update the State_Context and re-evaluate scheme eligibility
5. THE System SHALL support all Indian states and union territories in the State_Context

### Requirement 3: Dynamic Eligibility Matching

**User Story:** As a user, I want the system to match me with relevant government schemes, so that I can discover programs I qualify for.

#### Acceptance Criteria

1. WHEN user context is available, THE Eligibility_Matcher SHALL query Bedrock_Service with user information and scheme database
2. WHEN evaluating eligibility, THE Eligibility_Matcher SHALL consider at least 30 central government schemes
3. WHERE State_Context is available, THE Eligibility_Matcher SHALL include state-specific schemes in the evaluation
4. WHEN Bedrock_Service returns matching schemes, THE System SHALL rank them by relevance to the user's context
5. WHEN no schemes match initially, THE System SHALL proceed to ask clarifying questions before concluding no matches exist

### Requirement 4: Progressive Clarifying Questions

**User Story:** As a user who provided incomplete information, I want the system to ask me simple yes/no questions, so that I can easily provide additional details.

#### Acceptance Criteria

1. WHEN user context is insufficient for accurate matching, THE Clarification_Engine SHALL generate a yes/no question to gather missing information
2. WHEN generating questions, THE Clarification_Engine SHALL prioritize the most impactful information gaps first
3. WHEN a user answers a clarifying question, THE System SHALL update the user context and re-evaluate eligibility
4. THE Clarification_Engine SHALL limit clarifying questions to a maximum of 5 per session to avoid user fatigue
5. WHEN presenting questions, THE System SHALL use simple language appropriate for low-literacy users

### Requirement 5: Simple Explanations and Guidance

**User Story:** As a user, I want to understand matched schemes in simple terms, so that I can decide which programs to pursue.

#### Acceptance Criteria

1. WHEN displaying a matched scheme, THE System SHALL provide a simple explanation in the user's selected language
2. WHEN showing scheme details, THE System SHALL include the benefits, basic eligibility criteria, and application steps
3. WHEN available, THE System SHALL provide official documentation links for each scheme
4. WHEN displaying information, THE System SHALL use visual icons to enhance comprehension for low-literacy users
5. THE System SHALL present information in short, digestible sections rather than long paragraphs

### Requirement 6: Low-Bandwidth and Offline Support

**User Story:** As a user in a rural area with poor internet connectivity, I want the system to work on slow connections and cache information, so that I can access schemes despite connectivity challenges.

#### Acceptance Criteria

1. WHEN the system detects slow network conditions, THE System SHALL automatically enable Low_Bandwidth_Mode
2. WHILE in Low_Bandwidth_Mode, THE System SHALL minimize data transfer by compressing responses and limiting media
3. WHEN scheme information is retrieved, THE System SHALL cache it locally for offline access
4. WHEN a user is offline, THE System SHALL provide access to previously cached scheme information
5. WHEN connectivity is restored, THE System SHALL synchronize any pending queries or updates

### Requirement 7: Anonymous Session Management

**User Story:** As a privacy-conscious user, I want my session to be saved without requiring personal identification, so that I can return to my results without compromising privacy.

#### Acceptance Criteria

1. WHEN a user starts interacting, THE System SHALL create an anonymous Session with a unique identifier
2. WHEN a Session is created, THE System SHALL store user context and matched schemes without collecting personally identifiable information
3. WHEN a user returns with a Session identifier, THE System SHALL restore their previous context and results
4. THE System SHALL retain anonymous Session data for a maximum of 30 days
5. WHEN a Session expires, THE System SHALL permanently delete all associated data

### Requirement 8: Shareable Summaries

**User Story:** As a user who found relevant schemes, I want to share or save a summary, so that I can reference it later or help others.

#### Acceptance Criteria

1. WHEN a user completes their query, THE System SHALL generate a Summary containing matched schemes and next steps
2. WHEN a Summary is generated, THE System SHALL create a shareable link that works without authentication
3. WHEN a Summary is accessed via link, THE System SHALL display the scheme information in a readable format
4. THE Summary SHALL include scheme names, brief descriptions, eligibility criteria, and application links
5. WHEN generating a Summary, THE System SHALL include visual icons for easy recognition

### Requirement 9: Accessibility and Inclusion

**User Story:** As a user with disabilities or special needs, I want the system to be accessible, so that I can use it regardless of my abilities.

#### Acceptance Criteria

1. THE System SHALL comply with WCAG 2.1 Level AA accessibility standards for web interfaces
2. WHEN using screen readers, THE System SHALL provide appropriate ARIA labels and semantic HTML
3. THE System SHALL support keyboard-only navigation for all interactive elements
4. WHEN displaying visual content, THE System SHALL provide text alternatives for images and icons
5. THE System SHALL maintain sufficient color contrast ratios for users with visual impairments

### Requirement 10: Responsible Disclaimers and Transparency

**User Story:** As a user relying on AI-generated information, I want clear disclaimers about the system's limitations, so that I understand when to seek official verification.

#### Acceptance Criteria

1. WHEN a user first accesses the system, THE System SHALL display a disclaimer about the AI-assisted nature of the service
2. WHEN showing scheme matches, THE System SHALL include a notice to verify eligibility with official sources
3. WHEN the system cannot determine eligibility with confidence, THE System SHALL explicitly state the uncertainty
4. THE System SHALL provide contact information for official government helplines or websites
5. WHEN displaying AI-generated content, THE System SHALL clearly indicate it is not official government communication

### Requirement 11: Nationwide Scalability

**User Story:** As a system administrator, I want the system to handle users from across India simultaneously, so that it can serve the entire nation effectively.

#### Acceptance Criteria

1. THE System SHALL support concurrent access by at least 10,000 users without performance degradation
2. WHEN user load increases, THE System SHALL scale infrastructure automatically to maintain response times
3. THE System SHALL maintain average response times under 5 seconds for scheme matching queries
4. WHEN integrating new schemes, THE System SHALL support adding schemes without system downtime
5. THE System SHALL maintain 99.5% uptime availability for nationwide access

### Requirement 12: Voice Output and Audio Responses

**User Story:** As a user with low literacy, I want to hear responses spoken aloud, so that I can understand the information without reading.

#### Acceptance Criteria

1. WHEN the system generates a response, THE Voice_Interface SHALL provide an option to hear it spoken aloud
2. WHEN text-to-speech is activated, THE Voice_Interface SHALL speak in the user's selected language
3. WHEN speaking responses, THE Voice_Interface SHALL use clear pronunciation and appropriate pacing for comprehension
4. THE System SHALL allow users to pause, replay, or skip audio responses
5. WHEN in Low_Bandwidth_Mode, THE Voice_Interface SHALL optimize audio quality for minimal data usage
