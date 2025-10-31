# Coding Challenge

## Overview

You are given a PHP snippet that fetches data from an API and returns formatted results. Your task is to implement this functionality in the provided project structure and write tests for it.

## Environment

- Composer and Docker Compose are pre-configured
- Tests run with `composer test` (uses Pest PHP framework)
- API server available via `docker-compose up -d api` (optional for testing)
- Code quality checks: `composer check` runs linting, static analysis, and tests

## The Code

Here is the code snippet to implement:

```php
<?php

class ApiFetcher
{
    private $url = 'http://localhost:8000';
    private $logFile = '/tmp/api_log.txt';

    public function getData()
    {
        $ch = curl_init();
        curl_setopt($ch, CURLOPT_URL, $this->url);
        curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
        $response = curl_exec($ch);
        
        if (!$response) {
            $this->log('Error fetching data: ' . curl_error($ch));
            return [];
        }

        $decoded = json_decode($response);
        curl_close($ch);

        if (!$decoded) {
            $this->log('Error decoding JSON');
            return [];
        }

        $results = [];
        foreach ($decoded as $item) {
            if ($item->active) {
                $results[] = strtoupper($item->name);
            }
        }

        return $results;
    }

    private function log($message)
    {
        file_put_contents($this->logFile, date('c') . ' ' . $message . PHP_EOL, FILE_APPEND);
    }
}

$fetcher = new ApiFetcher();
$data = $fetcher->getData();
print_r($data);
```

## Your Task

1. Implement this functionality in the `src/` directory using the `App\` namespace
2. Write tests in the `tests/` directory

## Constraints

- You may use any standard PHP 8.2+ features
- You may structure the code any way you want inside `src/`
- Feel free to add functionality/complexity if you need to. We want to know how complete of a solution you can provide with little context.
- If you need to add dependencies, make sure to justify them.
- It's not a rule, but try not to assign more than 60 mins to the task.

## Evaluation Criteria

Your solution will be evaluated based on correctness, code quality, testing and standards compliance.

## Submission

1. Implement your solution in the `src/` directory
2. Write tests in the `tests/` directory
3. Remove or update the example files as needed
4. Invite the @gonzalo-nr github user into your repo
5. Create a Pull Request to the default branch with your changes

### PR Description

In your Pull Request description, please briefly document:

- **Assumptions** you made (e.g., about API response structure, error handling, etc.)
- **Design decisions** and their rationale
- **Trade-offs** you considered (if any)

This helps us understand your thought process and decision-making approach.

Good luck!
